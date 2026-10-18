| Original Code | Optimized Code |
|---|---|
| `/*Xeon Phi offload code*/`<br>OpenMP Do loop starts<br><br>................<br><br>!$omp critical<br>&nbsp;&nbsp;if (used_img_map(img_j) .eq. 0) then<br>&nbsp;&nbsp;&nbsp;&nbsp;used_img_map(img_j) = 1<br>&nbsp;&nbsp;&nbsp;&nbsp;used_img_cnt = used_img_cnt + 1<br>&nbsp;&nbsp;&nbsp;&nbsp;used_img_lst(used_img_cnt) = img_j<br>&nbsp;&nbsp;end if<br>!$omp end critical<br><br>................<br>OpenMP loop ends<br>................<br><br>/*Xeon Phi and Host version of used_img_map() are combined. Similarly two versions of used_img_lst() are combined for later use*/ | `/*Xeon Phi offload code*/`<br>OpenMP Do loop starts<br><br>................<br><br>used_img_map(img_j) = 1<br><br>................<br>OpenMP loop ends<br>................<br><br>/*Xeon Phi version of used_img_map() is used with existing img_map() and used_img_lst() to get combined version of used_img_lst() used_img_map() for later use*/ |

# FIGURE 6.5

Code snippets to show the optimization of the assignment of neighboring atoms by removal of an omp critical section.

All of the tasks in the original code can be optimized by:

+   1. allocating a larger array of size *atm_cnt* × *number of threads*, allowing one allocation of the array during system setup, removing the need to reallocate on each loop iteration
+   2. One time initialization of the array in system setup
+   3. using this larger array with proper indexing in the neighbor list code
+   4. resetting only the positions of the larger array which have already been used. Thus, the array can be used again in the next time step.

With this optimization, we can save the time of resetting and allocating the array inside the OpenMP runtime in every time step; both of which are expensive. The optimized code can be found in get_nb_list_offload() routine inside nb_pairlist.F90 file.