# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

## [Unreleased]
- Added function to copy a Lisp string's content to a buffer `Value::copy_string_contents`.
- Deprecated `unwrap_or_propagate`, and marked it as `unsafe`.

## [0.11.0] - 2019-08-05
- Made `env.call` a lot more flexible. Also added `value.call`.
- Added `rust-wrong-type-user-ptr` to `wrong-type-argument` classification.
- Deprecated `emacs::module_init!` and `emacs::export_functions!`.
- Replaced`IntoLisp` implementation for `AsRef<str>` with separate implementations for `&str` and `&String`.

## [0.10.3] - 2019-07-24
- Made `#[defun]` function signatures display correctly in `help-mode` and `helpful-mode`.

## [0.10.2] - 2019-07-24
- Added `defun_prefix` option to `#[module]`.
- Fixed `#[defun]` not handling raw identifiers correctly.

## [0.10.1] - 2019-07-18
- Made `Vector::get` generic by return type.
- Added `FromLisp` and `IntoLisp` implementations for most integer types, and an optional feature `lossy-integer-conversion` to control their behavior. This allows them to be used in `#[defun]` signatures.
- Made `Env::message` take `AsRef<str>`, not just a `&str`.

## [0.10.0] - 2019-07-17
- Raise minimum supported Rust version to 1.36 (for `MaybeUninit`).
- Added `Vector` type to represent Lisp's vectors.
- Allowed `Rc` and `Arc` to be embedded in `user-ptr` by marking them as `Transfer`.
- Removed `libc` dependency.
- Removed `Transfer::finalizer`.
- Deprecated `env.is_not_nil(value)` in favor of `value.is_not_nil()`.
- Deprecated `env.eq(value1, value2)` in favor of `value1.eq(value2)`.
- Improved Lisp-to-Rust string conversion's performance by making utf-8 validation optional, behind a feature, `utf-8-validation`.
- Improved Rust-to-Lisp string conversion's performance by not creating a temporary `CString`.
- Fixed a safety bug in which short-lived references were allowed to be embedded in `user-ptr`.

## [0.9.0] - 2019-07-11
- `ResultExt` is now a collection of Emacs-specific extension methods for `Result`, instead of a re-export of `failure::ResultExt`.
- Added `failure` as a re-exported sub-module.
- Added `unwrap_or_propagate` for better panic handling: propagation of non-local exits without `Result`, and improved error messages.

## [0.8.0] - 2019-04-20
- Input parameters with reference types are now interpreted as Rust data structures embedded in `user-ptr` objects.
- Return values are now embedded in `user-ptr` objects if `user_ptr` option is specified.

## [0.7.0] - 2019-04-15
- Greatly improved ergonomics with attribute macros `#[[emacs::module]` and] `#[defun]`.
- Deprecated macros with `emacs_` prefix.
- Made `Value.env` public.
- Removed the need for user crate to depend directly on `libc`.
- Added lifetime parameter to `FromLisp`.

## [0.6.0] - 2019-03-26
- Upgraded to Rust 2018 edition.

## [0.5.2] - 2018-09-15
- New values obtained from `Env` are now GC-protected. This fixes memory issue #2.

## [0.5.1] - 2018-03-03
- Added `FromLisp` implementation for `Option`.
- Fixed `IntoLisp` not working on `Option<&str>`.

## [0.5.0] - 2018-02-24
- Error handling integration with other Rust crates is improved:
  + The exposed error type is now `failure::Error`.
  + `ErrorKind` enum now implements `failure::Fail`.
- Redundant variants of `ErrorKind` were removed.
- Errors in Rust code now signal custom error types to Lisp:
  + `rust-error`
  + `rust-wrong-type-user-ptr`
- Panics are now caught and signaled to Lisp as a special error type: `rust-panic`.
- `env.is_not_nil` and `env.eq` now return `bool` instead of `Result`.

## [0.4.0] - 2018-02-18
- APIs now take `&Env` instead of `&mut Env`.
- `Value`s are no longer passed by reference, and are lifetime-scoped by `Env`.
- Data conversion:
  + Conversion is now simply `.into_rust()` and `.into_lisp(env)`.
  + `RefCell`, `Mutex`, `RwLock` can be directly transferred to Lisp.
  + Many built-in types are now supported.
- Function declaration:
  + Signatures of exportable functions are now simplified to `fn(&CallEnv) -> Result<T>`.
  + `emacs_subrs!` is replaced by `emacs_export_functions!`.
  + `emacs_lambda!` can be used to create Lisp lambdas.
- Panics no longer unwind into C.
- Load/test scripts now work in Linux.

## [0.3.0] - 2018-01-09
- Values of Rust types that implement `Transfer` can be embedded in Lisp objects.
- Wrapper types `Env` and `Value` are now used instead of raw types.

## [0.2.0] - 2018-01-04
New reworked version

[Unreleased]: https://github.com/ubolonton/emacs-module-rs/compare/0.11.0...HEAD
[0.11.0]: https://github.com/ubolonton/emacs-module-rs/compare/0.10.3...0.11.0
[0.10.3]: https://github.com/ubolonton/emacs-module-rs/compare/0.10.2...0.10.3
[0.10.2]: https://github.com/ubolonton/emacs-module-rs/compare/0.10.1...0.10.2
[0.10.1]: https://github.com/ubolonton/emacs-module-rs/compare/0.10.0...0.10.1
[0.10.0]: https://github.com/ubolonton/emacs-module-rs/compare/0.9.0...0.10.0
[0.9.0]: https://github.com/ubolonton/emacs-module-rs/compare/0.8.0...0.9.0
[0.8.0]: https://github.com/ubolonton/emacs-module-rs/compare/0.7.0...0.8.0
[0.7.0]: https://github.com/ubolonton/emacs-module-rs/compare/0.6.0...0.7.0
[0.6.0]: https://github.com/ubolonton/emacs-module-rs/compare/0.5.2...0.6.0
[0.5.2]: https://github.com/ubolonton/emacs-module-rs/compare/0.5.1...0.5.2
[0.5.1]: https://github.com/ubolonton/emacs-module-rs/compare/0.5.0...0.5.1
[0.5.0]: https://github.com/ubolonton/emacs-module-rs/compare/0.4.0...0.5.0
[0.4.0]: https://github.com/ubolonton/emacs-module-rs/compare/0.3.0...0.4.0
[0.3.0]: https://github.com/ubolonton/emacs-module-rs/compare/bcf0546...0.3.0
[0.2.0]: https://github.com/ubolonton/emacs-module-rs/compare/772bc3b...bcf0546
