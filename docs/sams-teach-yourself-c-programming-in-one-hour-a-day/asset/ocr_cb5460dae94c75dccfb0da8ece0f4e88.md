# Understanding Linked Lists

409

```
94:    }
95:    else    * it is being added to the middle or end */
96:    {
97:        tmp_rec = first->next_rec;
98:        prev_rec = first;
99: 
100:        * Check to see where link is added. *
101:    {
102:        if ( tmp_rec == NULL )
103:            {
104:                * we are adding second record to end */
105:                prev_rec->next_rec = new_rec;
106:            }
107:        else
108:            {
109:                * check to see if adding in middle */
110:                while ( ( tmp_rec->next_rec != NULL))
111:                    {
112:                        if ( new_rec->ch < tmp_rec->ch )
113:                            {
114:                                new_rec->next_rec = tmp_rec;
115:                                if (new_rec->next_rec != prev_rec->next_rec)
116:                                    {
117:                                        printf("ERROR*");
118:                                        get(stdin);
119:                                        exit(0);
120:                                    }
121:                                prev_rec->next_rec = new_rec;
122:                                break;      /* link is added, exit while */
123:                            }
124:                        else
125:                            {
126:                                tmp_rec = tmp_rec->next_rec;
127:                                prev_rec = prev_rec->next_rec;
128:                            }
129:                    }
130:                }
131:            * check to see if adding to the end */
132:            if (tmp_rec->next_rec == NULL)
133:                {\n134:                    if (new_rec->ch < tmp_rec->ch ) /* 1 b4 end */
135:                        {\n136:                            new_rec->next_rec = tmp_rec;
137:                            prev_rec->next_rec = new_rec;
138:                        }
139:                    else      /* at the end */
140:                        {\n141:                            tmp_rec->next_rec = new_rec;
142:                            new_rec->next_rec = NULL;      /* redundant *//
143:                        }
144:                }
```

16