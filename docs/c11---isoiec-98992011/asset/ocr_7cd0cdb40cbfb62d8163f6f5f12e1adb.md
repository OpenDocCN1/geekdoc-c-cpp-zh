# 6.10.8.3 Conditional macros

The following macros are conditionally defined by the implementation:

+   - __STC_ANALYZABLE__ The integer constant 1, intended to indicate conformance to the specifications in annex L (Analyability).

+   - __STC_IEC_559__ The integer constant 1, intended to indicate conformance to the specifications in annex F (IEC 60559 floating-point arithmetic).

+   - __STC_IEC_559_COMPLEX__ The integer constant 1, intended to indicate adherence to the specifications in annex G (IEC 60559 compatible complex arithmetic).

+   - __STC_LIB_EXT1__ The integer constant 2011L, intended to indicate support for the extensions in annex K (Bounds-checking interfaces).¹79)

+   - __STC_NO_ATOMICS__ The integer constant 1, intended to indicate that the implementation does not support atomic types (including the _Atomic stdatomic.h header).

+   - __STC_NO_COMPLEX__ The integer constant 1, intended to indicate that the implementation does not support complex types or the <complex.h> header.

+   - __STC_NO_THREADS__ The integer constant 1, intended to indicate that the implementation does not support the <threads.h> header.

+   - __STC_NO_VLA__ The integer constant 1, intended to indicate that the implementation does not support variable arrays or variably modified types.

An implementation that defines __STC_NO_COMPLEX__ shall not define __STC_IEC_559_COMPLEX__

> 179) The intention is that this will remain an integer type of long int that is increased with each revision of this International Standard.