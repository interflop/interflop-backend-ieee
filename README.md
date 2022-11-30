# interflop-backend-ieee

## Arguments
The IEEE backend implements straighforward IEEE-754 arithmetic.
It should have no effect on the output and behavior of your program.

The options `--debug` and `--debug_binary` enable verbose output that print
every instrumented floating-point operation.

The option `--count-op` enable to count the dynamic number of mul/div/add/sub operations during the instrumented program execution, 
and print it on the standard error output at the end of program execution.
```bash

VFC_BACKENDS="libinterflop_ieee.so --help" ./test
Info [verificarlo]: loaded backend libinterflop_ieee.so
Usage: libinterflop_ieee.so [OPTION...]

  -b, --debug-binary         enable binary debug output
  -d, --debug                enable debug output
  -n, --print-new-line       add a new line after debug ouput
  -o, --count-op             enable operation count output
  -p, --print-subnormal-normalized
                             normalize subnormal numbers
  -s, --no-backend-name      do not print backend name in debug output
  -?, --help                 Give this help list
      --usage                Give a short usage message

VFC_BACKENDS="libinterflop_ieee.so --debug" ./test
Info [verificarlo]: loaded backend libinterflop_ieee.so
Info [interflop_ieee]: Decimal 1.23457e-05 - 9.87654e+12 -> -9.87654e+12
Info [interflop_ieee]: Decimal 1.23457e-05 * 9.87654e+12 -> 1.21933e+08
Info [interflop_ieee]: Decimal 1.23457e-05 / 9.87654e+12 -> 1.25e-18
...

VFC_BACKENDS="libinterflop_ieee.so --debug-binary --print-new-line" ./test
Info [verificarlo]: loaded backend libinterflop_ieee.so
Info [interflop_ieee]: Binary
+1.100111100100000011000001011001111111010000011 x 2^-17 -
+1.00011111011100011111010100010000111 x 2^43 ->
-1.00011111011100011111010100010000111 x 2^43

Info [interflop_ieee]: Binary
+1.100111100100000011000001011001111111010000011 x 2^-17 *
+1.00011111011100011111010100010000111 x 2^43 ->
+1.110100010010001011111111111110000011000100100110111 x 2^26

Info [interflop_ieee]: Binary
+1.100111100100000011000001011001111111010000011 x 2^-17 /
+1.00011111011100011111010100010000111 x 2^43 ->
+1.0111000011101111100001010101101010010010111010010101 x 2^-60
...

VFC_BACKENDS="libinterflop_ieee.so --count-op" ./test
Info [verificarlo]: loaded backend libinterflop_ieee.so
result is correct -9.87642e+12 == -9.87642e+12 (ref)
operations count:
         mul=2
         div=2
         add=4
         sub=2

```
