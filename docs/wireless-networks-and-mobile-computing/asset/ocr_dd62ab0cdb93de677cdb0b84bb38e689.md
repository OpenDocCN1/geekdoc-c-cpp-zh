# TABLE 9.3: Pipeline stages for design proposed in [18]

\begin{tabular}{cccccc}
1st stage & _i_<sub>1</sub> = _i_<sub>0</sub> + 1 & _i_<sub>2</sub> = _i_<sub>1</sub> + 1 & _i_<sub>3</sub> = _i_<sub>2</sub> + 1 &  &  \\
2nd stage &  & Read _S_[_i_<sub>1</sub>] & Read _S_[_i_<sub>2</sub>] & Read _S_[_i_<sub>3</sub>] &  \\
 &  & Store _S_[_i_<sub>1</sub>] into _SI_ & Store _S_[_i_<sub>2</sub>] into _SI_ & Store _S_[_i_<sub>3</sub>] into _SI_ &  \\
 &  & _j_<sub>1</sub> = _j_<sub>0</sub> + _S_[_i_<sub>1</sub>] & _j_<sub>2</sub> = _j_<sub>1</sub> + _S_[_i_<sub>2</sub>] & _j_<sub>3</sub> = _j_<sub>2</sub> + _S_[_i_<sub>3</sub>] &  \\
3rd stage &  &  & Read _S_[_j_<sub>1</sub>] & Read _S_[_j_<sub>2</sub>] & Read _S_[_j_<sub>3</sub>] \\
 &  &  & Store _S_[_j_<sub>1</sub>] in _SJ_ & Store _S_[_j_<sub>2</sub>] in _SJ_ & Store _S_[_j_<sub>3</sub>] in _SJ_ \\
 &  &  & _t_<sub>1</sub> = _SI_ + _S_[_j_<sub>1</sub>] & _t_<sub>2</sub> = _SI_ + _S_[_j_<sub>2</sub>] & _t_<sub>3</sub> = _SI_ + _S_[_j_<sub>3</sub>] \\
 &  &  & Write _SI_ into _S_[_j_<sub>1</sub>] & Write _SI_ into _S_[_j_<sub>2</sub>] & Write _SI_ into _S_[_j_<sub>3</sub>] \\
4th stage &  &  &  & Read _S_[_t_<sub>1</sub>] & Read _S_[_t_<sub>2</sub>] \\
 &  &  &  & Store _S_[_t_<sub>1</sub>] into _K_ & Store _S_[_t_<sub>2</sub>] into _K_ \\
 &  &  &  &  & Store _S_[_t_<sub>3</sub>] into _K_ \\
 &  &  &  & Write _SJ_ into _S_[_i_<sub>1</sub>] & Write _SJ_ into _S_[_i_<sub>2</sub>] \\
 &  &  &  &  & Write _SJ_ into _S_[_i_<sub>3</sub>] \\
\end{tabular}