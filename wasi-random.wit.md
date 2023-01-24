# WASI Random API

WASI Random is a random data API.

It is intended to be portable at least between Unix-family platforms and
Windows.

## `get-random-bytes`
```wit
/// Return `len` random bytes.
///
/// This function must produce data from an adaquately seeded
/// cryptographically-secure pseudo-random number generator (CSPRNG), so it
/// must not block, from the perspective of the calling program, and the
/// returned data is always unpredictable.
///
/// Deterministic environments must omit this function, rather than
/// implementing it with deterministic data.
get-random-bytes: func(len: u32) -> list<u8>
```

## `get-random-u64`
```wit
/// Return a random `u64` value.
///
/// This function returns the same type of random data as `get-random-bytes`,
/// represented as a `u64`.
get-random-u64: func() -> u64
```

## `insecure-random`
```wit
/// Return a value containing 128 random bits.
///
/// In the future, this will likely be replaced by a value import, to prevent
/// it from being called multiple times and potentially used for purposes
/// other than DoS protection.
///
/// The returned value is not required to be computed from a CSPRNG, and may 
/// even be entirely deterministic. Host implementatations are encouraged to 
/// provide random values to any program exposed to attacker-controlled 
/// content, to enable DoS protection built into many languages' hash-map 
/// implementations.
insecure-random: func() -> tuple<u64, u64>
```
