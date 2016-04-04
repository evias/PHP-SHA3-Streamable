# Streamable SHA-3 in pure PHP!

* SHA3-224
* SHA3-256 (for 128-bit security like SHA2-256)
* SHA3-384
* SHA3-512 (for 256-bit security like SHA2-512)


Unbounded output:

* SHAKE128 (Use at least 256 bits of output for 128-bit security)
* SHAKE256 (Use at least 512 bits of output for 256-bit security)


**NEW: Use 64-bit PHP for best performance, because native 64-bit integers will be used. (Only supported on PHP 5.6.3 or later)** 64-bit mode is more than 4 times faster in PHP 5.6.

Amazingly, PHP 5.2 (EOL in January 2011) as well as PHP 7.0 is supported.
Please report if you find a problem.

Note that SHA-3 is considably slower than SHA-2 in *software*, not to mention
PHP's notable slowness. PHP 7.0 is 4x the speed of PHP 5.6.


## Usage
Namespaced class `desktopd\SHA3\Sponge` is available at the `namespaced/` directory of this repository. **This is the optimized version.**

        <?php
        use desktopd\SHA3\Sponge as SHA3;
        require __DIR__ . '/namespaced/desktopd/SHA3/Sponge.php';
        
        $sponge = SHA3::init (SHA3::SHA3_512);
        $sponge->absorb ('');
        // fixed size (512 bits) output
        echo bin2hex ($sponge->squeeze ()), PHP_EOL;
        // a69f73cca23a9ac5c8b567dc185a756e97c982164fe25859e0d1dcc1475c80a615b2123af1f5f94c11e3e9402c3ac558f500199d95b6d3e301758586281dcd26

### PHP 5.2 (legacy)
Use `SHA3.php` **(slower)**:

        <?php
        require dirname (__FILE__) . '/SHA3.php';
        
        $shake128 = SHA3::init (SHA3::SHAKE128);
        $shake128->absorb ('The quick brown fox ');
        $shake128->absorb ('jumps over the lazy dog');
        // Squeeze 256 bits of hash output!
        echo bin2hex ($shake128->squeeze (32)) . PHP_EOL;
        // f4202e3c5852f9182a0430fd8144f0a74b95e7417ecae17db0f8cfeed0e3e66e
        // more output possible


## TODO
* Optimize for speed, while defending against timing attacks (SHA-3 is good at that)
* Implemented: Faster operations with 64-bit PHP using the native integer type


## Legal

README.markdown:
Copyright (C) 2016 Desktopd Developers

Copying and distribution of this file, with or without modification,
are permitted in any medium without royalty provided the copyright
notice and this notice are preserved.


PHP-SHA3-Streamable is free software. The library (the files `SHA3.php` and
`namespaced/desktopd/SHA3/Sponge.php`) is under GNU LGPL version 3 or later.
Other codes are under GNU GPL version 3 or later.
See the files COPYING.LGPL (GNU LGPL) and COPYING (GNU GPL) for copying
conditions.
