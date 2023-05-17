# XL-FFT

A formula-based Fast Fourier Transform for Excel.

Calculate real and complex Fourier transforms of one-dimensional arrays in Excel without VBA macros.


## Installation

The recommended installation method is Microsoft's _Advanced Formula Environment_ for Excel (now part of [Excel Labs](https://www.microsoft.com/en-us/garage/profiles/excel-labs/)).
Create a new module (the suggested name is `FFT`, but any name will work) and paste the contents of the file `XL-FFT.xlf` in the text area, or import a new module directly from [this gist](https://gist.github.com/altomani/0b56cb0eac5a0b083620b8471fc76271).

Alternatively, it is also possible to copy the individual definition of `LAMBDA` formulas into the Excel Name manager, after removing all comments (and the trailing semicolons).


## Usage

The Fourier Transform operates on real and complex vectors. Complex numbers are represented as a pair of horizontally adjacent real numberrs. A complex number $z=x+\mathrm{i}y$ is represented as:

```
  | A | B |
--|---|---|
1 | x | y |
```


Vectors are always column vectors. For example a real vector `(x_1, x_2)` is represented as:

```
  |  A  |
--|-----|
1 | x_1 |
2 | x_2 |
```

and a complex vector `(z_1, z_2) = (x_1 + i*y_1, x_2 + i*y_2)` as:

```
  |  A  |  B  |
--|-----|-----|
1 | x_1 | y_1 |
2 | x_2 | y_2 |
```


### Complex Fourier Transform

**Forward Fourier Transform**

```
FFT(z, [n])
```

Compute the Fourier transform of `z`,
where `z` is a complex vector and `n` is the length of the transform. If the length of `z` is smaller than `n` then `z` is padded with zeroes; if it is larger than `n` then `z` is truncated, if it is equal to `n` or if `n` is omitted, then `z` is not modified. The output is a complex vector of length `n`. The output is a complex vector of length `n`.

**Inverse Fourier Transform**

```
IFFT(z, [n])
```

Compute the inverse Fourier transform of `z`,
where `z` is a complex vector and `n` is the length of the transform. If the length of `z` is smaller than `n` then `z` is padded with zeroes; if it is larger than `n` then `z` is truncated, if it is equal to `n` or if `n` is omitted, then `z` is not modified. The output is a complex vector of length `n`.

There are different conventions for the norm of the forward and inverse transform. Here the forward transform has norm `n` and the inverse transform has norm `1/n`.


### Real Fourier Transform

**Forward Fourier Transform**

```
RFFT(x, [n])
```

Compute the Fourier transform of `x`,
where `x` is a real vector and `n` is the length of the real vector on which the transform is applied. 
If the length of `x` is smaller than `n` then `z` is padded with zeroes; if it is larger than `n` then `x` is truncated, if it is equal to `n` or if `n` is omitted, then `x` is not modified. The output is a complex vector of length `(n + 2) / 2` if `n` is even and `(n + 1) / 2` if `n` is odd. 

**Inverse Fourier Transform**

```
IRFFT(z, [n])
```

Compute the inverse Fourier transform of `z`,
where `z` is a complex vector and `n` is the length of the real transform of `z`. If the length of `z` is smaller than `(n + 2) / 2` (if `n` is even) or `(n + 1) / 2` (if `n` is odd) then `z` is padded with zeroes; if it is larger then `z` is truncated, if it is equal then `z` is not modified, if `n` is omitted then it is set to twice the length of `z` minus one and `z` is not modified. The output is a real vector of length `n`. Note that it is necessary to specify `n` in order to obtain an output of odd length.

The convention for the norm is the same as in the complex case.

## License

Released under the MIT license. See the file `LICENSE`.