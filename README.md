# D bindings for lapack

## Example usage: SVD


```
#!/usr/bin/env dub
/+ dub.json:
{
    "name": "testlapack",
    "dependencies": {"lapacke": "~>0.1.2"},
}
+/

/*
*  Compile example:
*  dub run --single testlapack.d
*/

import std.stdio : writefln;
import lapack;
import std.datetime : StopWatch;

void main()
{
	double[] a = [
			      8.79,  6.11, -9.15,  9.57, -3.49,  9.84,
            9.93,  6.91, -7.93,  1.64,  4.02,  0.15,
            9.83,  5.04,  4.86,  8.83,  9.80, -8.99,
            5.45, -0.27,  4.85,  0.74, 10.00, -6.02,
            3.16,  7.98,  3.01,  5.80,  4.27, -5.31
	];
  enum m = 5;
  enum n = 6;
  int info = 0; 
  double[m] s;
  double[m*m] u;
  double[m*n] vt;
  double[m-1] superb;
  int output = gesvd(RowMajor, 'A', 'A', m, n, a.ptr, n, s.ptr, u.ptr, m, vt.ptr, n, superb.ptr );
  writefln("Outputs: \n%s\n%s\n%s", s, u, vt);
}
```

The [`dstep`](https://github.com/jacob-carlborg/dstep) D package was very useful in converting this library.
