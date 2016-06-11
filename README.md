# libpcl

This is my fork of Portable Coroutine Library (http://www.xmailserver.org/pcl.html) with a few bugfixes.

The problem of original pcl-1.12 code is incorrect estimation of minimal buffer size for stack (CO_MIN_SIZE) in `pcl_private.h`.
PCL-1.12 believe that `CO_MIN_SIZE` = 4K is always enough, but it is not so.

For example, on aarch64 the `struct sigcontext` reserves at least 4K just "for FP/SIMD state and future expansion" (see `<asm/sigcontext.h>` for aarch64).
 
So, I need more accurate way to estimate memory buffer sizes for coroutine stacks.

Additionally, I added the `co_get_min_stack_size()` routine to original API to allow application get known minimal memory requirements for coroutine stack buffers.
     

