---
title: "go-dsp documentation"
linkTitle: "Home"
type: docs
cascade:
  type: docs
description: "Digital signal processing in pure Go (CGO=0): filter design and filtering, spectral estimation and resampling, with the semantics of SciPy's scipy.signal."
---

**go-dsp is digital signal processing in pure Go.** Its first library,
`signal`, provides filter design (IIR and FIR, windows), filtering and
zero-phase filtering, convolution, spectral estimation, resampling and peak
finding, with the semantics of SciPy's `scipy.signal` and, where it differs, a
note on MATLAB's. Its tests replay recorded answers of SciPy 1.18.1, and its
documentation records the maximum error in ULPs and the time against SciPy on
one core, case by case.

## The libraries

| Library | Status | What it does |
| --- | --- | --- |
| [signal]({{< relref "signal" >}}) | released v0.1.0 | IIR design (Butterworth, Chebyshev, elliptic, Bessel), FIR design (window method, `Remez`, `Firls`), windows, filtering and zero-phase filtering, convolution, Welch, STFT and Lomb–Scargle estimation, resampling, peak finding |

Wavelets and audio I/O are planned in this organisation and are not started.

## Install

```sh
go get github.com/go-dsp/signal@v0.1.0
```

The module needs the Go toolchain its `go.mod` names and is pure Go
(`CGO_ENABLED=0`).

## What the pages hold

| Library | Pages |
| --- | --- |
| signal | [overview]({{< relref "signal" >}}) · [verification]({{< relref "signal/verification" >}}) · [accuracy]({{< relref "signal/accuracy" >}}) · [performance]({{< relref "signal/performance" >}}) |

## Built on

`signal` depends on [go-fft/fft](https://github.com/go-fft/fft) (transforms and
the classic windows), [go-numerics/special](https://github.com/go-numerics/special)
(complete elliptic integrals, `I0`) and
[go-simd/floats](https://github.com/go-simd/floats) (the assembly dot product
used by the FIR kernels).
