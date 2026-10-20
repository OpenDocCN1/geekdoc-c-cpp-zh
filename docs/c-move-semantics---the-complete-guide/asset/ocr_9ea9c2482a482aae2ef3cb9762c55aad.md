# 11 Perfect Passing with auto&&

10.3.2 Conflicting Template Parameter Deduction with Universal References . . . . . . 167

10.3.3 Pure RValue References of Generic Types . . . . . . . . . . . . . . . . . . . . 168

10.4 Nasty Details of Perfect Forwarding . . . . . . . . . . . . . . . . . . . . . . . . 169

10.4.1 “Universal” versus “Forwarding” Reference . . . . . . . . . . . . . . . . . . 169

10.4.2 Why && for Both Ordinary Rvalues and Universal References? . . . . . . . . 170

10.5 Summary . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 171

11.1 Default Perfect Passing . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 173

11.1.1 Default Perfect Passing in Detail . . . . . . . . . . . . . . . . . . . . . . . 173

11.2 Universal References with auto&& . . . . . . . . . . . . . . . . . . . . . . . . 175

11.2.1 Type Deduction of auto&& . . . . . . . . . . . . . . . . . . . . . . . . . . . . 176

11.2.2 Perfectly Forwarding an auto&& Reference . . . . . . . . . . . . . . . . . . 177

11.3 auto&& as Non-Forwarding Reference . . . . . . . . . . . . . . . . . . . . . . . 178

11.3.1 Universal References and the Range-Based for Loop . . . . . . . . . . . . . 178

11.4 Perfect Forwarding in Lambdas . . . . . . . . . . . . . . . . . . . . . . . . . . 182

11.5 Using auto&& in C++20 Function Declarations . . . . . . . . . . . . . . . . . . 183

11.6 Summary . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 183

# 12 Perfect Returning with decltype(auto)

12.1 Perfect Returning . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 185

12.2 decltype(auto) . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 186

12.2.1 Return Type decltype(auto) . . . . . . . . . . . . . . . . . . . . . . . . . . 187

12.2.2 Deferred Perfect Returning . . . . . . . . . . . . . . . . . . . . . . . . . . 189

12.2.3 Perfect Forwarding and Returning with Lambdas . . . . . . . . . . . . . . 191

12.3 Summary . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 192

# Part III: Move Semantics in the C++ Standard Library

# 13 Move-Only Types

13.1 Declaring and Using Move-Only Types . . . . . . . . . . . . . . . . . . . . . . 195