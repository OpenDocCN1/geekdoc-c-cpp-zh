```
void g_object_unref(GObject *object) {
    gint oref;
    oref = g_atomic_int_get(&object->ref_count);
    if (oref > 1) {
        g_atomic_int_add(&object->ref_count, -1);
    } else {
        oref = g_atomic_int_add(&object->ref_count, -1);
        if (oref == 1) {
            object->klass->finalize(object);
            g_type_free_instance(object);
        }
    }
}

void g_emblem_class_init(GEmblemClass *klass) {
    klass->finalize = g_emblem_finalize;
}

void g_emblem_finalize(GObject *object) {
    GEmblem *emblem = (GEmblem*)object;
    g_object_unref(emblem->icon);
}
```

# Figure 10. Managed types example from glib-2.0 library

directly exploit the structural subtyping relationship and consider all structural subtypes of the input to DecRef as being managed. We compare these two approaches in section 8.2.

# 7.3 Interprocedural Reference Count Manipulation

Not all functions directly increment and decrement references. Many use auxiliary functions, particularly those that rely on atomic increments and decrements. We employ a simple analysis to summarize the effects that functions have on the integer fields of their pointer-typed arguments. This analysis also tracks these effects for arguments of type int* to accommodate reference counting functions that pass the address of their reference count field instead of the object containing it.

# 7.4 Benefits of Automation

For users unfamiliar with a library, the inferred annotations document that reference counts must be maintained. More importantly, automatically finding the vast majority of reference-counted types decreases a potentially large annotation burden.

# 8. Evaluation

We have applied the analyses described in sections 3 to 6 to a suite of fifteen open-source libraries. The libraries range in size from a few functions and a few hundred lines of code up to several thousand functions with hundreds of thousands of lines of code.

We evaluate the effectiveness of the ownership transfer analysis and the reference counting analysis separately. For the most part, libraries using a reference counting discipline do not require the results of the ownership transfer analysis because ownership is explicitly shared through the reference counts. Thus, the results of the ownership transfer analysis are typically not necessary to generate library bindings for reference-counted libraries.

# 8.1 Transfer Analysis

This section evaluates the effectiveness of the ownership transfer analysis, with a particular focus on the reduction in manual annota-

# Table 1. Number of inferred transfer and escape annotations

| Library Analyzed | Transferred Parameters | | | | |
|---|---|---|---|---|---|
| Name | Functions | Transfer | Contract | Indirect | Direct |
| archive | 267 | 9 | 33 | 18 | 47 |
| freenect | 61 | 2 | 0 | 5 | 13 |
| fuse | 188 | 4 | 5 | 106 | 28 |
| glpk | 1072 | 0 | 67 | 54 | 149 |
| gsl | 3910 | 39 | 68 | 21 | 88 |
| ical | 1045 | 10 | 0 | 7 | 142 |

tion burden compared to relying solely on the results of an escape analysis. Table 1 shows the number of inferred annotations for six libraries of various sizes. The transfer analysis was designed based on archive and ical. The remaining libraries can be considered as the test set. The second column in the table notes the number of functions in each library. The “Transfer” column reports the number of function parameters that our analysis has identified as transferring ownership from the caller. The rest of the columns break down the results of our escape analysis.

We partition escaping parameters into three categories: contract escapes, indirect escapes, and direct escapes. Contract escapes are parameters that escape through calls to function pointers where some targets are known, and all of those targets agree that the parameter does not escape. We refer to these parameters as contract escapes because they only escape if the contract on the function pointer they are passed to is violated, i.e., only if the assumptions of section 6 do not apply. Indirect escapes are parameters that are passed as arguments to calls through function pointers for which no targets can be identified. However, it is rare in practice for parameters to truly escape through function pointers because that would make the code difficult to reason about. If a consumer of these analysis results can make this assumption, the distinction can make a significant difference. For example, the fuse client library has many more indirect escapes than direct escapes. Direct escapes in table 1 are the remaining escaping parameters: simple escapes, such as to global variables, that are not due to calls through function pointers.

While contract escapes are clearly not expected to escape by the library, by virtue of library-provided initializers, they offer more information still. Each indirect function call that induces contract escapes imposes a contract on the function pointer that is dereferenced for that call. We can say that any function that could be pointed to by that function pointer should obey the contract that its arguments not escape. Contract escapes are most prevalent in libraries with polymorphic behavior, as can be seen in archive. In this library, polymorphism is implemented through function pointers stored in each object. These function pointer fields are initialized with functions defined in the library when objects are created, allowing us to infer the corresponding contracts as suggested in section 6. It is important to note that we do not consider an argument to an indirect function call to be a contract escape if we merely know some of the targets of the call. We only label it as a contract escape if all known call targets agree that the parameter does not escape.

Each transfer annotation has an accompanying direct escape annotation. If the results of the ownership transfer analysis, rather than the escape analysis, are used to automate resource management, then the difference between the “Direct” and “Transfer” columns in table 1 is the number of manual annotations saved by the ownership transfer analysis. Without the ownership transfer analysis, each extra escape annotation introduces a memory leak that must be plugged with a manual annotation. This difference is striking in glpk and ical: the ownership transfer analysis saves over 100 manual annotations in each. Further, glpk does not seem to ever transfer ownership. However, as discussed in section 5, the escape annotations are still useful as object lifetime documentation to the user.