
```c
typedef lval*(*builtin)(lenv*, lval);

struct lval {
  int type;

  /* 基础 / */
  long num;
  char* err;
  char* sym;
  char* str;

  /* 函数 / */
  lval*(*builtin)(lenv*, lval);
  lenv* env;
  lval** formals;
  lval* body;

  /* 表达式 / */
  int count;
  lval** cell;
};

lval* lval_num(long x) {
  lval* v = malloc(sizeof(lval));
  v->type = LVAL_NUM;
  v->num = x;
  return v;
}

lval* lval_err(char* fmt, ... ) {
  lval* v = malloc(sizeof(lval));
  v->type = LVAL_ERR;
  va_list va;
  va_start(va, fmt);
  v->err = malloc(512);
  vprintfprintf(v->err, 512, fmt, va);
  va_end(va);
  return v;
}

lval* lval_sym(char* s) {
  lval* v = malloc(sizeof(lval));
  v->type = LVAL_SYM;
  v->sym = malloc(strlen(s) + 1);
  strcpy(v->sym, s);
  return v;
}

lval* lval_str(char* s) {
  lval* v = malloc(sizeof(lval));
  v->type = LVAL_STR;
  v->str = malloc(strlen(s) + 1);
  strcpy(v->str, s);
  return v;
}

lval* lval_builtin(builtin func) {
  lval* v = malloc(sizeof(lval));
  v->type = LVAL_FUN;
  v->builtin = func;
  return v;
}

lenv* lenv_new(void);

lval* lval_lambda(lval* formals, lval* body) {
  lval* v = malloc(sizeof(lval));
  v->type = LVAL_FUN;
  v->builtin = NULL;
  v->formals = strdup(formals);
  v->body = body;
  return v;
}

lval* lval_sexpr(void) {
  lval* v = malloc(sizeof(lval));
  v->type = LVAL_SEXPR;
  v->count = 0;
  v->cell = NULL;
  return v;
}

lval* lval_getpr(void) {
  lval* v = malloc(sizeof(lval));
  v->type = LVAL_SEXPR;
  v->count = 0;
  v->cell = NULL;
  return v;
}

void lval_del(lval* v) {
  switch (v->type) {
    case LVAL_NUM: break;
    case LVAL_FUN:
      if (v->builtin) {
        lenv_del(v->env);
        lval_del(v->formals);
      }
      lval_del(v->body);
      break;
    case LVAL_ERR: free(v->err); break;
    case LVAL_SYM: free(v->sym); break;
    case LVAL_STR: free(v->str); break;
    case LVAL_SEXPR:
      for (int i = 0; i < v->count; i++) {
        lval_del(v->cell[i]);
      }
      free(v->cell);
      break;
  }
  free(v);
}

lval* lval_copy(lval* v) {
  lval* x = malloc(sizeof(lval));
  x->type = v->type;
  switch (v->type) {
    case LVAL_FUN:
      if (v->builtin) {
        x->builtin = v->builtin;
      } else {
        x->builtin = NULL;
        x->env = lenv_copy(v->env);
        x->formals = lval_copy(v->formals);
        x->body = lval_copy(v->body);
      }
      break;
    case LVAL_NUM: x->num = v->num; break;
    case LVAL_ERR:
      x->err = malloc(strlen(v->err) + 1);
      strcpy(x->err, v->err);
      break;
    case LVAL_SYM:
      x->sym = malloc(strlen(v->sym) + 1);
      strcpy(x->sym, v->sym);
      break;
    case LVAL_STR:
      x->str = malloc(strlen(v->str) + 1);
      strcpy(x->str, v->str);
      break;
    case LVAL_SEXPR:
    case LVAL_QEXPR:
      x->count = v->count;
      x->cell = malloc(sizeof(lval*) * x->count);
      for (int i = 0; i < x->count; i++) {
        x->cell[i] = lval_copy(v->cell[i]);
      }
      break;
  }
  return x;
}

lval* lval_add(lval* v, lval* x) {
  v->count++;
  v->cell = realloc(v->cell, sizeof(lval*) * v->count);
  v->cell[v->count-1] = x;
  return v;
}

lval* lval_join(lval* x, lval* y) {
  for (int i = 0; i < y->count; i++) {
    lval_add(x, y->cell[i]);
  }
  free(y->cell);
  free(y);
  return x;
}

lval* lval_pop(lval* v, int i) {
  lval* x = v->cell[i];
  memmove(v->cell[i], v->cell[i+1], sizeof(lval*) * (v->count-i-1));
  v->count--;
  v->cell = realloc(v->cell, sizeof(lval*) * v->count);
  return x;
}

lval* lval_take(lval* v, int i) {
  lval* x = lval_pop(v, i);
  lval_del(v);
  return x;
}

void lval_print(lval* v, char* open, char close) {
  putchar(open);
  for (int i = 0; i < v->count; i++) {
    lval_print(v->cell[i]);
    if (i != v->count-1) {
      putchar(' ');
    }
  }
  putchar(close);
}

void lval_print_str(lval* v) {
    /* 复制字符串 */
    char* escaped = malloc(strlen(v->str)+1);
    strcpy(escaped, v->str);
    /* 通过转义函数处理 */
    escaped = mfc_escape(escaped);
    /* 打印字符 */
    printf("\"s\"", escaped);
    /* 释放复制的字符串 */
    free(escaped);
}

void lval_print(lval* v) {
    switch (v->type) {
        case LVAL_FUN:
            if (v->builtin) {
                printf("builtin");
            } else {
                printf("{");
                lval_print(v->formals);
                putchar(' ');
                lval_print(v->body);
                putchar('}');
            }
            break;
        case LVAL_NUM:
            printf("%d", v->num); break;
        case LVAL_ERR:
            printf("Error: %s", v->err); break;
        case LVAL_SYM:
            printf("%s", v->sym); break;
        case LVAL_STR:
            lval_print_str(v); break;
        case LVAL_EXPR:
            lval_print(v->expr, '{', '}'); break;
        case LVAL_QEXPR:
            lval_print(v->expr, '(', ')'); break;
    }
}

int lval_eq(lval* x, lval* y) {
    if (x->type != y->type) {
        return 0;
    }
    switch (x->type) {
        case LVAL_NUM: return (x->num == y->num);
        case LVAL_ERR: return (strcmp(x->err, y->err) == 0);
        case LVAL_SYM: return (strcmp(x->sym, y->sym) == 0);
        case LVAL_STR: return (strcmp(x->str, y->str) == 0);
        case LVAL_FUN:
            if (x->builtin && y->builtin) {
                return x->builtin == y->builtin;
            } else {
                return lval_eq(x->formals, y->formals) && lval_eq(x->body, y->body);
            }
        case LVAL_QEXPR:
            if (x->count != y->count) {
                return 0;
            }
            for (int i = 0; i < x->count; i++) {
                if (!lval_eq(x->cell[i], y->cell[i])) {
                    return 0;
                }
            }
            return 1;
        break;
    }
    return 0;
}

char* ltype_name(int t) {
switch(t) {
    case LVAL_FUN: return "Function";
    case LVAL_NUM: return "Number";
    case LVAL_ERR: return "Error";
    case LVAL_SYM: return "Symbol";
    case LVAL_STR: return "String";
    case LVAL_EXPR: return "S-Expression";
    case LVAL_QEXPR: return "Q-Expression";
    default: return "Unknown";
}

// 列表 lenv /

struct lenv {
  lenv* par;
  int count;
  char** syms;
  lval** vals;
};

lenv* lenv_new(void) {
  lenv* e = malloc(sizeof(lenv));
  e->par = NULL;
  e->count = 0;
  e->syms = NULL;
  e->vals = NULL;
  return e;
}

void lenv_del(lenv* e) {
  for (int i = 0; i < e->count; i++) {
    free(e->syms[i]);
    lval_del(e->vals[i]);
  }
  free(e->syms);
  free(e->vals);
  free(e);
}

lenv* lenv_copy(lenv* e) {
  lenv* n = malloc(sizeof(lenv));
  n->par = e->par;
  n->count = e->count;
  n->syms = malloc(sizeof(char*) as e->count);
  n->vals = malloc(sizeof(lval*) * e->count);
  for (int i = 0; i < e->count; i++) {
    n->syms[i] = strdup(e->syms[i]);
    n->vals[i] = lval_copy(e->vals[i]);
  }
  return n;
}

lenv* lenv_get(lenv* e, char* s) {
  for (int i = 0; i < e->count; i++) {
    if (strcmp(e->syms[i], s) == 0) {
      return e->vals[i];
    }
  }
  return NULL;
}

void lenv_put(lenv* e, char* s, lval* v) {
  e->count++;
  e->syms = realloc(e->syms, sizeof(char*) * e->count);
  e->vals = realloc(e->vals, sizeof(lval*) * e->count);
  e->syms[e->count-1] = strdup(s);
  e->vals[e->count-1] = v;
}

void lenv_def(lenv* e, char* k, lval* v) {
    while (e->par) { e = e->par; }
    lenv_put(e, k, v);
}

// 内置函数 /

#define LASSERT(args, cond, fet, ...) \
if ((cond)) { lval* err = lval_err(fet, #__VA_ARGS__); lval_del(args); return err; }

#define LASSERT_TYPE(func, args, index, expect) \
LASSERT(args, args->cell[index]->type == expect, \
    fprintf("%%s passed incorrect argument. Got %s, Expected %s.", \
    func, index, lype_name(args->cell[index]->type), lype_name(expect)));

#define LASSERT_NUM(func, args, num) \
LASSERT(args, args->count == num, \
    fprintf("%%s passed incorrect number of arguments. Got %d, Expected %d.", \
    func, args->count, num));

#define LASSERT_NOT_EMPTY(func, args, index) \
LASSERT(args, args->cell[index]->count == 0, \
    fprintf("%%s passed incorrect for argument %d.", \
    func, index));
```
