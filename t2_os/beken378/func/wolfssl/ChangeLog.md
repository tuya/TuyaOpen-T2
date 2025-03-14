# wolfSSL Release 4.1.0 (07/22/2019)

Release 4.1.0 of wolfSSL embedded TLS has bug fixes and new features including:

* A fix for the check on return value when verifying PKCS7 bundle signatures, all users with applications using the function wc_PKCS7_VerifySignedData should update
* Adding the function wc_PKCS7_GetSignerSID for PKCS7 firmware bundles as a getter function for the signers SID
* PKCS7 callback functions for unwrapping of CEK and for decryption
* Adding the error value PKCS7_SIGNEEDS_CHECK when no certificates are available in a PKCS7 bundle to verify the signature
* TLS 1.3 fixes including if major version is TLS Draft then it is now ignored and if version negotiation occurs but none were matched then an alert is now sent
* Addition of the WOLFSSL_PSK_ONE_ID macro for indicating that only one identity in TLS 1.3 PSK is available and will be cached
* Adding sanity checks on length of PSK identity from a TLS 1.3 pre-shared key extension
* Additional sanity checks and alert messages added for TLS 1.3
* Adding XTIME_MS macro to simplify the tls13.c time requirement
* Improvements and refactoring of code related to parsing and creating TLS 1.3 client hello packets
* TLS 1.3 version renegotiation now happens before interpreting ClientHello message
* Chacha20 algorithm optimizations on the ARM architecture for performance increase
* Poly1305 algorithm performance enhancements for the ARM architecture using the SIMD NEON extension
* Curve25519 and Ed25519 optimized for ARM architecture for performance increase
* SHA-512/384 optimizations for performance with ARM architecture using the SIMD NEON extension
* Sniffer updates including adding support for the null cipher and static ECDH key exchange and new SSLWatchCb callback
* Cipher suite TLS_RSA_WITH_NULL_MD5 for use with the sniffer (off by default)
* Sniffer statistic print outs with the macro WOLFSSL_SNIFFER_STATS defined
* A fix for wolfSSL_DH_generate_key when WOLFSSL_SMALL_STACK is defined
* wolfSSL_BN_Init implementation for opensslextra builds
* Updates to the function wolfSSL_i2d_RSAPrivateKey and additional automated tests
* Fixes for EVP_CipherFinal edge cases to match behavior desired
* Check for appropriate private vs public flag with ECC key decode in wolfSSL_EC_KEY_LoadDer_ex, thanks to Eric Miller for the report
* Implementation of the function wolfSSL_PEM_write_DHparams
* wolfSSL_RAND_seed is called in wolfSSL_Init now when opensslextra is enabled
* CryptoCell-310 support on nRF52840 added
* Fixes for atmel_ecc_create_pms to free the used slot.
* Fixes for building ATECC with ATCAPRINTF or WOLFSSL_PUBLIC_MP
* Cortex-M code changes to support IAR compiler
* Improvements to STM32 AES-GCM performance
* Fixes for 16-bit systems including PK callbacks, ATECC and LowResTimer function ptoto.
* IAR-EWARM compiler warning fix
* Clean up of user_settings for CS+ port
* Updating Renesas example projects to the latest version
* Micrium updates adjusting static macro name and added inline flag
* Fixes for building with WOLFSSL_CUSTOM_CURVES on Windows
* Updates and refactor to the default build settings with Arduino
* Fixes for visibility tags with Cygwin build
* STSAFE Improvements to support wolfSSL Crypto Callbacks
* Improvements to NetBSD builds and mutex use in test case
* Updating TI hardware offload with WOLFSSL_TI_CRYPT build
* Maintaining Xilinx FreeRTOS port by adjusting time.h include in wolfSSL
* SiFive HiFive E31 RISC‐V core family port
* Port for Telit IoT AppZone SDK
* OCSP Response signed by issuer with identical SKID fix
* Fix for sending revoked certificate with OCSP
* Honor the status sent over connection with peers and do not perform an internal OCSP lookup
* Adding the build flag `--enable-ecccustcurves=all` to enable all curve types
* Support add for Ed25519ctx and Ed25519ph sign/verify algorithms as per RFC 8032
* Addition of the macro WOLFSSL_NO_SIGALG to disable signature algorithms extension
* wc_AesCtrEncrypt in place addition, where input and output buffer can be the same buffer
* Single shot API added for SHA3; wc_Sha3_224Hash, wc_Sha3_256Hash, wc_Sha3_384Hash, wc_Sha3_512Hash
* Function additions for JSSE support some of which are wolfSSL_get_ciphers_iana and wolfSSL_X509_verify along with expansion of the --enable-jni option
* Macro guards for more modular SHA3 build (i.e. support for 384 size only)
* Benchmarking -thread <num> argument support for asynchronous crypto
* Blake2s support (--enable-blake2s), which provides 32-bit Blake2 support
* Macro SHA256_MANY_REGISTERS addition to potentially speed up SHA256 depending on architecture
* Additional TLS alert messages sent with the macro WOLFSSL_EXTRA_ALERTS defined
* Feature to fail resumption of a session if the session’s cipher suite is not in the client’s list, this can be overridden by defining the macro NO_RESUME_SUITE_CHECK
* Fallback SCSV (Signaling Cipher Suite Value) support on Server only (--enable-fallback-scsv)
* DTLS export state only (wolfSSL_dtls_export_state_only) which is a subset of the information exported from previous DTLS export function
* Function wc_DhCheckPubValue added to perform simple validity checks on DH keys
* Support for RSA SHA-224 signatures with TLS added
* Additional option “-print” to the benchmark app for printing out a brief summary after benchmarks are complete
*  Adding (--disable-pkcs12) option and improvements for disabled sections in pwdbased.c, asn.c, rsa.c, pkcs12.c and wc_encrypt
* Added DES3 support to the wolfSSL crypto callbacks
* Compile time fixes for build case with SP math and RSA only
* Fixes for Coverity static analysis report including explicit initialization of reported stack variables some additional Coverity fixes added thanks to Martin
* Fixes for scan build warnings (i.e possible null dereference in ecc.c)
* Resetting verify send value with a call to wolfSSL_clear function
* Fix for extern with sp_ModExp_2048 when building with --cpp option
* Fix for typo issue with --enable-sp=cortexm
* Adding #pragma warning disable 4127 for tfm.c when building with Visual Studio
* Improvements to the maximum ECC signature calculations
* Improvements to TLS write handling in error cases which helps user application not go through with a wolfSSL_write attempt after a wolfSSL_read failure
* Fix for read directory functions with Windows (wc_ReadDirFirst and wc_ReadDirNext)
* Sanity check on index before accessing domain component buffer in call to wolfSSL_X509_NAME_get_entry
* Sending fatal alert from client side on version error
* Fix for static RSA cipher suite with PK callback and no loaded private key
* Fix for potential memory leak in error case with the function wc_DsaKeyToDer, thanks to Chris H. for the report
* Adjusting STRING_USER macro to remove includes of standard lib <string.h> or <stdio.h>
* Bug fix for checking wrong allocation assignment in the function wc_PBKDF2 and handling potential leak on allocation failure. This case is only hit when the specific call to malloc fails in the function wc_PBKDF2. Thanks to Robert Altnoeder (Linbit) for the report
* Improved length checks when parsing ASN.1 certificates
* extern "C" additions to header files that were missing them
* Improved checking of return values with TLS extension functions and error codes
* Removing redundant calls to the generate function when instantiating and reseeding DRBG
* Refactoring and improvements to autoconf code with consolidating AM_CONDITIONAL statements
* Improvements for handling error return codes when reading input from transport layer
* Improvements to efficiency of SNI extension parsing and error checking with ALPN parsing
* Macro WOLFSSL_DEBUG_TLS addition for printing out extension data being parsed during a TLS connection
* Adjustment of prime testing with --disable-fastmath builds


This release of wolfSSL includes a fix for 2 security vulnerabilities.

There is a fix for a potential buffer overflow case with the TLSv1.3 PSK extension parsing. This affects users that are enabling TLSv1.3 (--enable-tls13). Thanks to Robert Hoerr for the report. The CVE associated with the report is CVE-2019-11873.

There is a fix for the potential leak of nonce sizes when performing ECDSA signing operations. The leak is considered to be difficult to exploit but it could potentially be used maliciously to perform a lattice based timing attack against previous wolfSSL versions. ECC operations with --enable-sp and --enable-sp-asm are not affected, users with private ECC keys in other builds that are performing ECDSA signing operations should update versions of wolfSSL along with private ECC keys. Thanks to Ján Jančár from Masaryk University for the report.


# wolfSSL Release 4.0.0 (03/20/2019)

Release 4.0.0 of wolfSSL embedded TLS has bug fixes and new features including:

* Support for wolfCrypt FIPS v4.0.0, certificate #3389
* FIPS Ready Initiative
* Compatibility fixes for secure renegotiation with Chrome
* Better size check for TLS record fragment reassembly
* Improvements to non-blocking and handshake message retry support for DTLS
* Improvements to OCSP with ECDSA signers
* Added TLS server side secure renegotiation
* Added TLS Trusted CA extension
* Add support for the Deos Safety Critical RTOS
* OCSP fixes for memory management and initializations
* Fixes for EVP Cipher decryption padding checks
* Removal of null terminators on `wolfSSL_X509_print` substrings
* `wolfSSL_sk_ASN1_OBJCET_pop` function renamed to `wolfSSL_sk_ASN1_OBJECT_pop`
* Adjustment to include path in compatibility layer for evp.h and objects.h
* Fixes for decoding BER encoded PKCS7 contents
* TLS handshake now supports using PKCS #11 for private keys
* PKCS #11 support of HMAC, AES-CBC and random seeding/generation
* Support for named FFDHE parameters in TLS 1.2 (RFC 7919)
* Port to Zephyr Project
* Move the TLS PRF to wolfCrypt.
* Update to CMS KARI support
* Added ESP32 WROOM support
* Fixes and additions to the OpenSSL compatibility layer
* Added WICED Studio Support
* MDK CMSIS RTOS v2
* Xcode project file update
* Fixes for ATECC508A/ATECC608A
* Fixes issue with CA path length for self signed root CA's
* Fixes for Single Precision (SP) ASM when building sources directly
* Fixes for STM32 AES GCM
* Fixes for ECC sign with hardware to ensure the input is truncated
* Fixes for proper detection of PKCS7 buffer overflow case
* Fixes to handle degenerate PKCS 7 with BER encoding
* Fixes for TLS v1.3 handling of 6144 and 8192 bit keys
* Fixes for possible build issues with SafeRTOS
* Added `ECC_PUBLICKEY_TYPE` to the support PEM header types
* Added strict checking of the ECDSA signature DER encoding length
* Added ECDSA option to limit sig/algos in client_hello to key size with
  `USE_ECDSA_KEYSZ_HASH_ALGO`
* Added Cortex-M support for Single Precision (SP) math
* Added wolfCrypt RSA non-blocking time support
* Added 16-bit compiler support using --enable-16bit option
* Improved Arduino sketch example
* Improved crypto callback features
* Improved TLS benchmark tool
* Added new wrapper for snprintf for use with certain Visual Studio builds,
  thanks to David Parnell (Cambridge Consultants)

This release of wolfSSL includes a fix for 1 security vulnerability.

* Fixed a bug in tls_bench.c example test application unrelated to the crypto
  or TLS portions of the library. (CVE-2019-6439)


# wolfSSL Release 3.15.7 (12/26/2018)

Release 3.15.7 of wolfSSL embedded TLS has bug fixes and new features including:

* Support for Espressif ESP-IDF development framework
* Fix for XCode build with iPhone simulator on i386
* PKCS7 support for generating and verify bundles using a detached signature
* Fix for build disabling AES-CBC and enabling opensslextra compatibility layer
* Updates to sniffer for showing session information and handling split messages across records
* Port update for Micrium uC/OS-III
* Feature to adjust max fragment size post handshake when compiled with the macro WOLFSSL_ALLOW_MAX_FRAGMENT_ADJUST
* Adding the macro NO_MULTIBYTE_PRINT for compiling out special characters that embedded devices may have problems with
* Updates for Doxygen documentation, including PKCS #11 API and more
* Adding Intel QuickAssist v1.7 driver support for asynchronous crypto
* Adding Intel QuickAssist RSA key generation and SHA-3 support
* RSA verify only (--enable-rsavfy) and RSA public only (--enable-rsapub) builds added
* Enhancements to test cases for increased code coverage
* Updates to VxWorks port for use with Mongoose, including updates to the OpenSSL compatibility layer
* Yocto Project ease of use improvements along with many updates and build instructions added to the INSTALL file
* Maximum ticket nonce size was increased to 8
* Updating --enable-armasm build for ease of use with autotools
* Updates to internal code checking TLS 1.3 version with a connection
* Removing unnecessary extended master secret from ServerHello if using TLS 1.3
* Fix for TLS v1.3 HelloRetryRequest to be sent immediately and not grouped



This release of wolfSSL includes a fix for 1 security vulnerability.

Medium level fix for potential cache attack with a variant of Bleichenbacher’s attack. Earlier versions of wolfSSL leaked PKCS #1 v1.5 padding information during private key decryption that could lead to a potential padding oracle attack. It is recommended that users update to the latest version of wolfSSL if they have RSA cipher suites enabled and have the potential for malicious software to be ran on the same system that is performing RSA operations. Users that have only ECC cipher suites enabled and are not performing RSA PKCS #1 v1.5 Decryption operations are not vulnerable. Also users with TLS 1.3 only connections are not vulnerable to this attack. Thanks to Eyal Ronen (Weizmann Institute), Robert Gillham (University of Adelaide), Daniel Genkin (University of Michigan), Adi Shamir (Weizmann Institute), David Wong (NCC Group), and Yuval Yarom (University of Adelaide and Data61) for the report.

The paper for further reading on the attack details can be found at http://cat.eyalro.net/cat.pdf.


See INSTALL file for build instructions.
More info can be found on-line at http://wolfssl.com/wolfSSL/Docs.html


# wolfSSL Release 3.15.5 (11/07/2018)

Release 3.15.5 of wolfSSL embedded TLS has bug fixes and new features including:

* Fixes for GCC-8 warnings with strings
* Additional compatibility API’s added, including functions like wolfSSL_X509_CA_num and wolfSSL_PEM_read_X509_CRL
* Fixes for OCSP use with NGINX port
* Renamed the macro inline to WC_INLINE for inline functions
* Doxygen updates and formatting for documentation generation
* Added support for the STM32L4 with AES/SHA hardware acceleration
* Adds checking for critical extension with certificate Auth ID and the macro WOLFSSL_ALLOW_CRIT_SKID to override the check
* Added public key callbacks to ConfirmSignature function to expand public key callback support
* Added ECC and Curve25519 key generation callback support
* Fix for memory management with wolfSSL_BN_hex2bn function
* Added support for dynamic allocation of PKCS7 structure using wc_PKCS7_New and wc_PKCS7_Free
* Port to apache mynewt added in the directory wolfssl-3.15.5/IDE/mynewt/*
* OCSP stapling in TLS 1.3 additions
* Port for ASIO added with --enable-asio configure flag
* Contiki port added with macro WOLFSSL_CONTIKI
* Memory free optimizations with adding in earlier free’s where possible
* Made modifications to the primality testing so that the Miller-Rabin tests check against up to 40 random numbers rather than a fixed list of small primes
* Certificate validation time generation updated
* Fixes for MQX classic 4.0 with IAR-EWARM
* Fix for assembly optimized version of Curve25519
* Make SOCKET_PEER_CLOSED_E consistent between read and write cases
* Relocate compatibility layer functions for OpenSSH port update
* Update to Intel® SGX port, files included by Windows version and macros defined when using WOLFSSL_SGX
* Updates to Nucleus version supported
* Stack size reduction with smallstack build
* Updates to Rowley-Crossworks settings for CMSIS 4
* Added reference STSAFE-A100 public key callbacks for TLS support
* Added reference ATECC508A/ATECC608A public key callbacks for TLS support
* Updated support for latest CryptoAuthLib (10/25/2018)
* Added a wolfSSL static library project for Atollic TrueSTUDIO
* Flag to disable AES-CBC and have only AEAD cipher suites with TLS
* AF_ALG and cryptodev-linux crypto support added
* Update to IO callbacks with use of WOLFSSL_BIO
* Additional support for parsing certificate subject OIDs (businessCategory, jurisdiction of incorporation country, and jurisdiction of incorporation state)
* Added  wc_ecc_ecport_ex and wc_export_inti API's for ECC hex string exporting
* Updates to XCODE build with wolfSSL
* Fix for guard on when to include sys/time.h header
* Updates and enhancements to the GCC-ARM example
* Fix for PKCS8 padding with encryption
* Updates for wolfcrypt JNI wrapper
* ALT_ECC_SIZE use with SP math
* PIC32MZ hardware acceleration buffer alignment fixes
* Renesas e2studio project files added
* Renesas RX example project added
* Fix for DH algorithm when using SP math with ARM assembly
* Fixes and enhancements for NXP K82 support
* Benchmark enhancements to print in CSV format and in Japanese
* Support for PKCS#11 added with --enable-pkcs11
* Fixes for asynchronous crypto use with TLS 1.3
* TLS 1.3 only build, allows for disabling TLS 1.2 and earlier protocols
* Fix for GCC warnings in function wolfSSL_ASN1_TIME_adj
* Added --enable-asn=nocrypt for certificate only parsing support
* Added support for parsing PIV format certificates with the function wc_ParseCertPIV and macro WOLFSSL_CERT_PIV
* Added APIs to support GZIP
* Updates to support Lighttpd
* Version resource added for Windows DLL builds
* Increased code coverage with additional testing
* Added support for constructed OCTET_STRING with PKCS#7 signed data
* Added DTLS either (server/client) side initialization setting
* Minor fixes for building with MINGW32 compiler
* Added support for generic ECC PEM header/footer with PKCS8 parsing
* Added Japanese output to example server and client with “-1 1” flag
* Added USE_ECDSA_KEYSZ_HASH_ALGO macro for building to use digest sizes that match ephemeral key size
* Expand PKCS#7 CMS support with KEKRI, PWRI and ORI
* Streaming capability for PKCS#7 decoding and sign verify added


See INSTALL file for build instructions.
More info can be found on-line at http://wolfssl.com/wolfSSL/Docs.html


# wolfSSL Release 3.15.3 (6/20/2018)

Release 3.15.3 of wolfSSL embedded TLS has bug fixes and new features including:

* ECDSA blinding added for hardening against side channel attacks
* Fix for compatibility layer build with no server and no client defined
* Use of optimized Intel assembly instructions on compatible AMD processor
* wolfCrypt Nucleus port additions
* Fix added for MatchDomainName and additional tests added
* Fixes for building with ‘WOLFSSL_ATECC508A’ defined
* Fix for verifying a PKCS7 file in BER format with indefinite size


This release of wolfSSL fixes 2 security vulnerability fixes.

Medium level fix for PRIME + PROBE attack combined with a variant of Lucky 13. Constant time hardening was done to avoid potential cache-based side channel attacks when verifying the MAC on a TLS packet. CBC cipher suites are susceptible on systems where an attacker could gain access and run a parallel program for inspecting caching. Only wolfSSL users that are using TLS/DTLS CBC cipher suites need to update. Users that have only AEAD and stream cipher suites set, or have built with WOLFSSL_MAX_STRENGTH (--enable-maxstrength), are not vulnerable. Thanks to Eyal Ronen, Kenny Paterson, and Adi Shamir for the report.

Medium level fix for a ECDSA side channel attack. wolfSSL is one of over a dozen vendors mentioned in the recent Technical Advisory “ROHNP” by author Ryan Keegan. Only wolfSSL users with long term ECDSA private keys using our fastmath or normal math libraries on systems where attackers can get access to the machine using the ECDSA key need to update.  An attacker gaining access to the system could mount a memory cache side channel attack that could recover the key within a few thousand signatures. wolfSSL users that are not using ECDSA private keys, that are using the single precision math library, or that are using ECDSA offloading do not need to update. (blog with more information https://www.wolfssl.com/wolfssh-and-rohnp/)


See INSTALL file for build instructions.
More info can be found on-line at http://wolfssl.com/wolfSSL/Docs.html

# wolfSSL Release 3.15.0 (06/05/2018)

Release 3.15.0 of wolfSSL embedded TLS has bug fixes and new features including:

* Support for TLS 1.3 Draft versions 23, 26 and 28.
* Add FIPS SGX support!
* Single Precision assembly code added for ARM and 64-bit ARM to enhance performance.
* Improved performance for Single Precision maths on 32-bit.
* Improved downgrade support for the TLS 1.3 handshake.
* Improved TLS 1.3 support from interoperability testing.
* Added option to allow TLS 1.2 to be compiled out to reduce size and enhance security.
* Added option to support Ed25519 in TLS 1.2 and 1.3.
* Update wolfSSL_HMAC_Final() so the length parameter is optional.
* Various fixes for Coverity static analysis reports.
* Add define to use internal struct timeval (USE_WOLF_TIMEVAL_T).
* Switch LowResTimer() to call XTIME instead of time(0) for better portability.
* Expanded OpenSSL compatibility layer with a bevy of new functions.
* Added Renesas CS+ project files.
* Align DH support with NIST SP 800-56A, add wc_DhSetKey_ex() for q parameter.
* Add build option for CAVP self test build (--enable-selftest).
* Expose mp_toradix() when WOLFSSL_PUBLIC_MP is defined.
* Example certificate expiration dates and generation script updated.
* Additional optimizations to trim out unused strings depending on build options.
* Fix for DN tag strings to have “=” when returning the string value to users.
* Fix for wolfSSL_ERR_get_error_line_data return value if no more errors are in the queue.
* Fix for AES-CBC IV value with PIC32 hardware acceleration.
* Fix for wolfSSL_X509_print with ECC certificates.
* Fix for strict checking on URI absolute vs relative path.
* Added crypto device framework to handle PK RSA/ECC operations using callbacks, which adds new build option `./configure --enable-cryptodev` or `WOLF_CRYPTO_DEV`.
* Added devId support to ECC and PKCS7 for hardware based private key.
* Fixes in PKCS7 for handling possible memory leak in some error cases.
* Added test for invalid cert common name when set with `wolfSSL_check_domain_name`.
* Refactor of the cipher suite names to use single array, which contains internal name, IANA name and cipher suite bytes.
* Added new function `wolfSSL_get_cipher_name_from_suite` for getting IANA cipher suite name using bytes.
* Fixes for fsanitize reports.
* Fix for openssl compatibility function `wolfSSL_RSA_verify` to check returned size.
* Fixes and improvements for FreeRTOS AWS.
* Fixes for building openssl compatibility with FreeRTOS.
* Fix and new test for handling match on domain name that may have a null terminator inside.
* Cleanup of the socket close code used for examples, CRL/OCSP and BIO to use single macro `CloseSocket`.
* Refactor of the TLSX code to support returning error codes.
* Added new signature wrapper functions `wc_SignatureVerifyHash` and `wc_SignatureGenerateHash` to allow direct use of hash.
* Improvement to GCC-ARM IDE example.
* Enhancements and cleanups for the ASN date/time code including new API's `wc_GetDateInfo`, `wc_GetCertDates` and `wc_GetDateAsCalendarTime`.
* Fixes to resolve issues with C99 compliance. Added build option `WOLF_C99` to force C99.
* Added a new `--enable-opensslall` option to enable all openssl compatibility features.
* Added new `--enable-webclient` option for enabling a few HTTP API's.
* Added new `wc_OidGetHash` API for getting the hash type from a hash OID.
* Moved `wolfSSL_CertPemToDer`, `wolfSSL_KeyPemToDer`, `wolfSSL_PubKeyPemToDer` to asn.c and renamed to `wc_`. Added backwards compatibility macro for old function names.
* Added new `WC_MAX_SYM_KEY_SIZE` macro for helping determine max key size.
* Added `--enable-enckeys` or (`WOLFSSL_ENCRYPTED_KEYS`) to enable support for encrypted PEM private keys using password callback without having to use opensslextra.
* Added ForceZero on the password buffer after done using it.
* Refactor unique hash types to use same internal values (ex WC_MD5 == WC_HASH_TYPE_MD5).
* Refactor the Sha3 types to use `wc_` naming, while retaining old names for compatibility.
* Improvements to `wc_PBKDF1` to support more hash types and the non-standard extra data option.
* Fix TLS 1.3 with ECC disabled and CURVE25519 enabled.
* Added new define `NO_DEV_URANDOM` to disable the use of `/dev/urandom`.
* Added `WC_RNG_BLOCKING` to indicate block w/sleep(0) is okay.
* Fix for `HAVE_EXT_CACHE` callbacks not being available without `OPENSSL_EXTRA` defined.
* Fix for ECC max bits `MAX_ECC_BITS` not always calculating correctly due to macro order.
* Added support for building and using PKCS7 without RSA (assuming ECC is enabled).
* Fixes and additions for Cavium Nitrox V to support ECC, AES-GCM and HMAC (SHA-224 and SHA3).
* Enabled ECC, AES-GCM and SHA-512/384 by default in (Linux and Windows)
* Added `./configure --enable-base16` and `WOLFSSL_BASE16` configuration option to enable Base16 API's.
* Improvements to ATECC508A support for building without `WOLFSSL_ATMEL` defined.
* Refactor IO callback function names to use `_CTX_` to eliminate confusion about the first parameter.
* Added support for not loading a private key for server or client when `HAVE_PK_CALLBACK` is defined and the private PK callback is set.
* Added new ECC API `wc_ecc_sig_size_calc` to return max signature size for a key size.
* Cleanup ECC point import/export code and added new API `wc_ecc_import_unsigned`.
* Fixes for handling OCSP with non-blocking.
* Added new PK (Primary Key) callbacks for the VerifyRsaSign. The new callbacks API's are `wolfSSL_CTX_SetRsaVerifySignCb` and `wolfSSL_CTX_SetRsaPssVerifySignCb`.
* Added new ECC API `wc_ecc_rs_raw_to_sig` to take raw unsigned R and S and encodes them into ECDSA signature format.
* Added support for `WOLFSSL_STM32F1`.
* Cleanup of the ASN X509 header/footer and XSTRNCPY logic.
* Add copyright notice to autoconf files. (Thanks Brian Aker!)
* Updated the M4 files for autotools. (Thanks Brian Aker!)
* Add support for the cipher suite TLS_DH_anon_WITH_AES256_GCM_SHA384 with test cases. (Thanks Thivya Ashok!)
* Add the TLS alert message unknown_psk_identity (115) from RFC 4279, section 2. (Thanks Thivya Ashok!)
* Fix the case when using TCP with timeouts with TLS. wolfSSL shall be agnostic to network socket behavior for TLS. (DTLS is another matter.) The functions `wolfSSL_set_using_nonblock()` and `wolfSSL_get_using_nonblock()` are deprecated.
* Hush the AR warning when building the static library with autotools.
* Hush the “-pthread” warning when building in some environments.
* Added a dist-hook target to the Makefile to reset the default options.h file.
* Removed the need for the darwin-clang.m4 file with the updates provided by Brian A.
* Renamed the AES assembly file so GCC on the Mac will build it using the preprocessor.
* Add a disable option (--disable-optflags) to turn off the default optimization flags so user may supply their own custom flags.
* Correctly touch the dummy fips.h header.

If you have questions on any of this, then email us at info@wolfssl.com.
See INSTALL file for build instructions.
More info can be found on-line at http://wolfssl.com/wolfSSL/Docs.html


# wolfSSL Release 3.14.0 (03/02/2018)

Release 3.14.0 of wolfSSL embedded TLS has bug fixes and new features including:

* TLS 1.3 draft 22 and 23 support added
* Additional unit tests for; SHA3, AES-CMAC, Ed25519, ECC, RSA-PSS, AES-GCM
* Many additions to the OpenSSL compatibility layer were made in this release. Some of these being enhancements to PKCS12, WOLFSSL_X509 use, WOLFSSL_EVP_PKEY, and WOLFSSL_BIO operations
* AVX1 and AVX2 performance improvements with ChaCha20 and Poly1305
* Added i.MX CAAM driver support with Integrity OS support
* Improvements to logging with debugging, including exposing more API calls and adding options to reduce debugging code size
* Fix for signature type detection with PKCS7 RSA SignedData
* Public key call back functions added for DH Agree
* RSA-PSS API added for operating on non inline buffers (separate input and output buffers)
* API added for importing and exporting raw DSA parameters
* Updated DSA key generation to be FIPS 186-4 compliant
* Fix for wolfSSL_check_private_key when comparing ECC keys
* Support for AES Cipher Feedback(CFB) mode added
* Updated RSA key generation to be FIPS 186-4 compliant
* Update added for the ARM CMSIS software pack
* WOLFSSL_IGNORE_FILE_WARN macro added for avoiding build warnings when not working with autotools
* Performance improvements for AES-GCM with AVX1 and AVX2
* Fix for possible memory leak on error case with wc_RsaKeyToDer function
* Make wc_PKCS7_PadData function available
* Updates made to building SGX on Linux
* STM32 hashing algorithm improvements including clock/power optimizations and auto detection of if SHA2 is supported
* Update static memory feature for FREERTOS use
* Reverse the order that certificates are compared during PKCS12 parse to account for case where multiple certificates have the same matching private key
* Update NGINX port to version 1.13.8
* Support for HMAC-SHA3 added
* Added stricter ASN checks to enforce RFC 5280 rules. Thanks to the report from Professor Zhenhua Duan, Professor Cong Tian, and Ph.D candidate Chu Chen from Institute of Computing Theory and Technology (ICTT) of Xidian University.
* Option to have ecc_mul2add function public facing
* Getter function wc_PKCS7_GetAttributeValue added for PKCS7 attributes
* Macros NO_AES_128, NO_AES_192, NO_AES_256 added for AES key size selection at compile time
* Support for writing multiple organizations units (OU) and domain components (DC) with CSR and certificate creation
* Support for indefinite length BER encodings in PKCS7
* Added API for additional validation of prime q in a public DH key
* Added support for RSA encrypt and decrypt without padding


See INSTALL file for build instructions.
More info can be found on-line at http://wolfssl.com/wolfSSL/Docs.html


# wolfSSL (Formerly CyaSSL) Release 3.13.0 (12/21/2017)

wolfSSL 3.13.0 includes bug fixes and new features, including support for
TLS 1.3 Draft 21, performance and footprint optimizations, build fixes,
updated examples and project files, and one vulnerability fix. The full list
of changes and additions in this release include:

* Fixes for TLS 1.3, support for Draft 21
* TLS 1.0 disabled by default, addition of “--enable-tlsv10” configure option
* New option to reduce SHA-256 code size at expense of performance
  (USE_SLOW_SHA256)
* New option for memory reduced build (--enable-lowresource)
* AES-GCM performance improvements on AVX1 (IvyBridge) and AVX2
* SHA-256 and SHA-512 performance improvements using AVX1/2 ASM
* SHA-3 size and performance optimizations
* Fixes for Intel AVX2 builds on Mac/OSX
* Intel assembly for Curve25519, and Ed25519 performance optimizations
* New option to force 32-bit mode with “--enable-32bit”
* New option to disable all inline assembly with “--disable-asm”
* Ability to override maximum signature algorithms using WOLFSSL_MAX_SIGALGO
* Fixes for handling of unsupported TLS extensions.
* Fixes for compiling AES-GCM code with GCC 4.8.*
* Allow adjusting static I/O buffer size with WOLFMEM_IO_SZ
* Fixes for building without a filesystem
* Removes 3DES and SHA1 dependencies from PKCS#7
* Adds ability to disable PKCS#7 EncryptedData type (NO_PKCS7_ENCRYPTED_DATA)
* Add ability to get client-side SNI
* Expanded OpenSSL compatibility layer
* Fix for logging file names with OpenSSL compatibility layer enabled, with
  WOLFSSL_MAX_ERROR_SZ user-overridable
* Adds static memory support to the wolfSSL example client
* Fixes for sniffer to use TLS 1.2 client method
* Adds option to wolfCrypt benchmark to benchmark individual algorithms
* Adds option to wolfCrypt benchmark to display benchmarks in powers
  of 10 (-base10)
* Updated Visual Studio for ARM builds (for ECC supported curves and SHA-384)
* Updated Texas Instruments TI-RTOS build
* Updated STM32 CubeMX build with fixes for SHA
* Updated IAR EWARM project files
* Updated Apple Xcode projects with the addition of a benchmark example project

This release of wolfSSL fixes 1 security vulnerability.

wolfSSL is cited in the recent ROBOT Attack by Böck, Somorovsky, and Young.
The paper notes that wolfSSL only gives a weak oracle without a practical
attack but this is still a flaw.  This release contains a fix for this report.
Please note that wolfSSL has static RSA cipher suites disabled by default as
of version 3.6.6 because of the lack of perfect forward secrecy.  Only users
who have explicitly enabled static RSA cipher suites with WOLFSSL_STATIC_RSA
and use those suites on a host are affected.  More information will be
available on our website at:

https://wolfssl.com/wolfSSL/security/vulnerabilities.php

See INSTALL file for build instructions.
More info can be found on-line at http://wolfssl.com/wolfSSL/Docs.html


# wolfSSL (Formerly CyaSSL) Release 3.12.2 (10/23/2017)

## Release 3.12.2 of wolfSSL has bug fixes and new features including:

This release includes many performance improvements with Intel ASM (AVX/AVX2) and AES-NI. New single precision math option to speedup RSA, DH and ECC. Embedded hardware support has been expanded for STM32, PIC32MZ and ATECC508A. AES now supports XTS mode for disk encryption. Certificate improvements for setting serial number, key usage and extended key usage. Refactor of SSL_ and hash types to allow openssl coexistence. Improvements for TLS 1.3. Fixes for OCSP stapling to allow disable and WOLFSSL specific user context for callbacks. Fixes for openssl and MySQL compatibility. Updated Micrium port. Fixes for asynchronous modes.

* Added TLS extension for Supported Point Formats (ec_point_formats)
* Fix to not send OCSP stapling extensions in client_hello when not enabled
* Added new API's for disabling OCSP stapling
* Add check for SIZEOF_LONG with sun and LP64
* Fixes for various TLS 1.3 disable options (RSA, ECC and ED/Curve 25519).
* Fix to disallow upgrading to TLS v1.3
* Fixes for wolfSSL_EVP_CipherFinal() when message size is a round multiple of a block size.
* Add HMAC benchmark and expanded AES key size benchmarks
* Added simple GCC ARM Makefile example
* Add tests for 3072-bit RSA and DH.
* Fixed DRAFT_18 define and fixed downgrading with TLS v1.3
* Fixes to allow custom serial number during certificate generation
* Add method to get WOLFSSL_CTX certificate manager
* Improvement to `wolfSSL_SetOCSP_Cb` to allow context per WOLFSSL object
* Alternate certificate chain support `WOLFSSL_ALT_CERT_CHAINS`. Enables checking cert against multiple CA's. 
* Added new `--disable-oldnames` option to allow for using openssl along-side wolfssl headers (without OPENSSL_EXTRA).
* Refactor SSL_ and hashing types to use wolf specific prefix (WOLFSSL and WC_) to allow openssl coexistence.
* Fixes for HAVE_INTEL_MULX
* Cleanup include paths for MySQL cmake build
* Added configure option for building library for wolfSSH (--enable-wolfssh)
* Openssl compatibility layer improvements
* Expanded API unit tests
* Fixes for STM32 crypto hardware acceleration
* Added AES XTS mode (--enable-xts)
* Added ASN Extended Key Usage Support (see wc_SetExtKeyUsage).
* Math updates and added TFM_MIPS speedup.
* Fix for creation of the KeyUsage BitString
* Fix for 8k keys with MySQL compatibility
* Fixes for ATECC508A.
* Fixes for PIC32MZ hashing.
* Fixes and improvements to asynchronous modes for Intel QuickAssist and Cavium Nitrox V.
* Update HASH_DRBG Reseed mechanism and add test case
* Rename the file io.h/io.c to wolfio.h/wolfio.c
* Cleanup the wolfIO_Send function.
* OpenSSL Compatibility Additions and Fixes
* Improvements to Visual Studio DLL project/solution.
* Added function to generate public ECC key from private key
* Added async blocking support for sniffer tool.
* Added wolfCrypt hash tests for empty string and large data.
* Added ability to use of wolf implementation of `strtok` using `USE_WOLF_STRTOK`.
* Updated Micrium uC/OS-III Port
* Updated root certs for OCSP scripts
* New Single Precision math option for RSA, DH and ECC (off by default). See `--enable-sp`.
* Speedups for AES GCM with AESNI (--enable-aesni)
* Speedups for SHA2, ChaCha20/Poly1035 using AVX/AVX2


# wolfSSL (Formerly CyaSSL) Release 3.12.0 (8/04/2017)

## Release 3.12.0 of wolfSSL has bug fixes and new features including:

- TLS 1.3 with Nginx! TLS 1.3 with ARMv8! TLS 1.3 with Async Crypto! (--enable-tls13)
- TLS 1.3 0RTT feature added
- Added port for using Intel SGX with Linux
- Update and fix PIC32MZ port
- Additional unit testing for MD5, SHA, SHA224, SHA256, SHA384, SHA512, RipeMd, HMAC, 3DES, IDEA, ChaCha20, ChaCha20Poly1305 AEAD, Camellia, Rabbit, ARC4, AES, RSA, Hc128
- AVX and AVX2 assembly for improved ChaCha20 performance
- Intel QAT fixes for when using --disable-fastmath
- Update how DTLS handles decryption and MAC failures
- Update DTLS session export version number for --enable-sessionexport feature
- Add additional input argument sanity checks to ARMv8 assembly port
- Fix for making PKCS12 dynamic types match
- Fixes for potential memory leaks when using --enable-fast-rsa
- Fix for when using custom ECC curves and add BRAINPOOLP256R1 test
- Update TI-RTOS port for dependency on new wolfSSL source files
- DTLS multicast feature added, --enable-mcast
- Fix for Async crypto with GCC 7.1 and HMAC when not using Intel QuickAssist
- Improvements and enhancements to Intel QuickAssist support
- Added Xilinx port
- Added SHA3 Keccak feature, --enable-sha3
- Expand wolfSSL Python wrapper to now include a client side implementation
- Adjust example servers to not treat a peer closed error as a hard error
- Added more sanity checks to fp_read_unsigned_bin function
- Add SHA224 and AES key wrap to ARMv8 port
- Update MQX classics and mmCAU ports
- Fix for potential buffer over read with wolfSSL_CertPemToDer
- Add PKCS7/CMS decode support for KARI with IssuerAndSerialNumber
- Fix ThreadX/NetX warning
- Fixes for OCSP and CRL non blocking sockets and for incomplete cert chain with OCSP
- Added RSA PSS sign and verify
- Fix for STM32F4 AES-GCM
- Added enable all feature (--enable-all)
- Added trackmemory feature (--enable-trackmemory)
- Fixes for AES key wrap and PKCS7 on Windows VS
- Added benchmark block size argument
- Support use of staticmemory with PKCS7
- Fix for Blake2b build with GCC 5.4
- Fixes for compiling wolfSSL with GCC version 7, most dealing with switch statement fall through warnings.
- Added warning when compiling without hardened math operations


Note:
There is a known issue with using ChaCha20 AVX assembly on versions of GCC earlier than 5.2. This is encountered with using the wolfSSL enable options --enable-intelasm and --enable-chacha. To avoid this issue ChaCha20 can be enabled with --enable-chacha=noasm.
If using --enable-intelasm and also using --enable-sha224 or --enable-sha256 there is a known issue with trying to use -fsanitize=address.

This release of wolfSSL fixes 1 low level security vulnerability.

Low level fix for a potential DoS attack on a wolfSSL client. Previously a client would accept many warning alert messages without a limit. This fix puts a limit to the number of warning alert messages received and if this limit is reached a fatal error ALERT_COUNT_E is returned. The max number of warning alerts by default is set to 5 and can be adjusted with the macro WOLFSSL_ALERT_COUNT_MAX. Thanks for the report from Tarun Yadav and Koustav Sadhukhan from Defence Research and Development Organization, INDIA.


See INSTALL file for build instructions.
More info can be found on-line at http://wolfssl.com/wolfSSL/Docs.html


# wolfSSL (Formerly CyaSSL) Release 3.11.1 (5/11/2017)

## Release 3.11.1 of wolfSSL is a TLS 1.3 BETA release, which includes:

- TLS 1.3 client and server support for TLS 1.3 with Draft 18 support

This is strictly a BETA release, and designed for testing and user feedback.
Please send any comments, testing results, or feedback to wolfSSL at
support@wolfssl.com.

See INSTALL file for build instructions.
More info can be found on-line at http://wolfssl.com/wolfSSL/Docs.html


# wolfSSL (Formerly CyaSSL) Release 3.11.0 (5/04/2017)

## Release 3.11.0 of wolfSSL has bug fixes and new features including:

- Code updates for warnings reported by Coverity scans
- Testing and warning fixes for FreeBSD on PowerPC
- Updates and refactoring done to ASN1 parsing functions
- Change max PSK identity buffer to account for an identity length of 128 characters
- Update Arduino script to handle recent files and additions
- Added support for PKCS#7 Signed Data with ECDSA
- Fix for interoperability with ChaCha20-Poly1305 suites using older draft versions
- DTLS update to allow multiple handshake messages in one DTLS record. Thanks to Eric Samsel over at Welch Allyn for reporting this bug.
- Intel QuickAssist asynchronous support (PR #715 - https://www.wolfssl.com/wolfSSL/Blog/Entries/2017/1/18_wolfSSL_Asynchronous_Intel_QuickAssist_Support.html)
- Added support for HAproxy load balancer
- Added option to allow SHA1 with TLS 1.2 for IIS compatibility (WOLFSSL_ALLOW_TLS_SHA1)
- Added Curve25519 51-bit Implementation, increasing performance on systems that have 128 bit types
- Fix to not send session ID on server side if session cache is off unless we're echoing 
session ID as part of session tickets
- Fixes for ensuring all default ciphers are setup correctly (see PR #830)
- Added NXP Hexiwear example in `IDE/HEXIWEAR`.
- Added wolfSSL_write_dup() to create write only WOLFSSL object for concurrent access
- Fixes for TLS elliptic curve selection on private key import.
- Fixes for RNG with Intel rdrand and rdseed speedups.
- Improved performance with Intel rdrand to use full 64-bit output
- Added new --enable-intelrand option to indicate use of RDRAND preference for RNG source 
- Removed RNG ARC4 support
- Added ECC helpers to get size and id from curve name.
- Added ECC Cofactor DH (ECC-CDH) support
- Added ECC private key only import / export functions.
- Added PKCS8 create function
- Improvements to TLS layer CTX handling for switching keys / certs.
- Added check for duplicate certificate policy OID in certificates.
- Normal math speed-up to not allocate on mp_int and defer until mp_grow
- Reduce heap usage with fast math when not using ALT_ECC_SIZE
- Fixes for building CRL with Windows
- Added support for inline CRL lookup when HAVE_CRL_IO is defined
- Added port for tenAsys INtime RTOS
- Improvements to uTKernel port (WOLFSSL_uTKERNEL2)
- Updated WPA Supplicant support
- Added support for Nginx
- Update stunnel port for version 5.40
- Fixes for STM32 hardware crypto acceleration
- Extended test code coverage in bundled test.c
- Added a sanity check for minimum authentication tag size with AES-GCM. Thanks to Yueh-Hsun Lin and Peng Li at KNOX Security at Samsung Research America for suggesting this.
- Added a sanity check that subject key identifier is marked as non-critical and a check that no policy OIDS appear more than once in the cert policies extension. Thanks to the report from Professor Zhenhua Duan, Professor Cong Tian, and Ph.D candidate Chu Chen from Institute of Computing Theory and Technology (ICTT) of Xidian University, China. Profs. Zhenhua Duan and Cong Tian are supervisors of Ph.D candidate Chu Chen.

This release of wolfSSL fixes 5 low and 1 medium level security vulnerability.

3 Low level fixes reported by Yueh-Hsun Lin and Peng Li from KNOX Security, Samsung Research America.
- Fix for out of bounds memory access in wc_DhParamsLoad() when GetLength() returns a zero. Before this fix there is a case where wolfSSL would read out of bounds memory in the function wc_DhParamsLoad.
- Fix for DH key accepted by wc_DhAgree when the key was malformed.
- Fix for a double free case when adding CA cert into X509_store.

Low level fix for memory management with static memory feature enabled. By default static memory is disabled. Thanks to GitHub user hajjihraf for reporting this.


Low level fix for out of bounds write in the function wolfSSL_X509_NAME_get_text_by_NID. This function is not used by TLS or crypto operations but could result in a buffer out of bounds write by one if called explicitly in an application. Discovered by Aleksandar Nikolic of Cisco Talos. http://talosintelligence.com/vulnerability-reports/

Medium level fix for check on certificate signature. There is a case in release versions 3.9.10, 3.10.0 and 3.10.2 where a corrupted signature on a peer certificate would not be properly flagged. Thanks to Wens Lo, James Tsai, Kenny Chang, and Oscar Yang at Castles Technology.


See INSTALL file for build instructions.
More info can be found on-line at http://wolfssl.com/wolfSSL/Docs.html


# wolfSSL (Formerly CyaSSL) Release 3.10.2 (2/10/2017)

## Release 3.10.2 of wolfSSL has bug fixes and new features including:

- Poly1305 Windows macros fix. Thanks to GitHub user Jay Satiro
- Compatibility layer expanded with multiple functions added
- Improve fp_copy performance with ALT_ECC_SIZE
- OCSP updates and improvements
- Fixes for IAR EWARM 8 compiler warnings
- Reduce stack usage with ECC_CACHE_CURVE disabled
- Added ECC export raw for public and private key
- Fix for NO_ASN_TIME build
- Supported curves extensions now populated by default
- Add DTLS build without big integer math
- Fix for static memory feature with wc_ecc_verify_hash_ex and not SHAMIR
- Added PSK interoperability testing to script bundled with wolfSSL
- Fix for Python wrapper random number generation. Compiler optimizations with Python could place the random number in same buffer location each time. Thanks to GitHub user Erik Bray (embray)
- Fix for tests on unaligned memory with static memory feature
- Add macro WOLFSSL_NO_OCSP_OPTIONAL_CERTS to skip optional OCSP certificates
- Sanity checks on NULL arguments added to wolfSSL_set_fd and wolfSSL_DTLS_SetCookieSecret
- mp_jacobi stack use reduced, thanks to Szabi Tolnai for providing a solution to reduce stack usage


This release of wolfSSL fixes 2 low and 1 medium level security vulnerability.

Low level fix of buffer overflow for when loading in a malformed temporary DH file. Thanks to Yueh-Hsun Lin and Peng Li from KNOX Security, Samsung Research America for the report.

Medium level fix for processing of OCSP response. If using OCSP without hard faults enforced and no alternate revocation checks like OCSP stapling then it is recommended to update.

Low level fix for potential cache attack on RSA operations. If using wolfSSL RSA on a server that other users can have access to monitor the cache, then it is recommended to update wolfSSL. Thanks to Andreas Zankl, Johann Heyszl and Georg Sigl at Fraunhofer AISEC for the initial report.

See INSTALL file for build instructions.
More info can be found on-line at http://wolfssl.com/wolfSSL/Docs.html


# wolfSSL (Formerly CyaSSL) Release 3.10.0 (12/21/2016)

## Release 3.10.0 of wolfSSL has bug fixes and new features including:

- Added support for SHA224
- Added scrypt feature
- Build for Intel SGX use, added in directory IDE/WIN-SGX
- Fix for ChaCha20-Poly1305 ECDSA certificate type request
- Enhance PKCS#7 with ECC enveloped data and AES key wrap support
- Added support for RIOT OS
- Add support for parsing PKCS#12 files
- ECC performance increased with custom curves
- ARMv8 expanded to AArch32 and performance increased
- Added ANSI-X9.63-KDF support
- Port to STM32 F2/F4 CubeMX
- Port to Atmel ATECC508A board
- Removed fPIE by default when wolfSSL library is compiled
- Update to Python wrapper, dropping DES and adding wc_RSASetRNG
- Added support for NXP K82 hardware acceleration
- Added SCR client and server verify check
- Added a disable rng option with autoconf
- Added more tests vectors to test.c with AES-CTR
- Updated DTLS session export version number
- Updated DTLS for 64 bit sequence numbers
- Fix for memory management with TI and WOLFSSL_SMALL_STACK
- Hardening RSA CRT to be constant time
- Fix uninitialized warning with IAR compiler
- Fix for C# wrapper example IO hang on unexpected connection termination


This release of wolfSSL fixes a low level security vulnerability. The vulnerability reported was a potential cache attack on RSA operations. If using wolfSSL RSA on a server that other users can have access to monitor the cache, then it is recommended to update wolfSSL. Thanks to Andreas Zankl, Johann Heyszl and Georg Sigl at Fraunhofer AISEC for the report. More information will be available on our site:

https://wolfssl.com/wolfSSL/security/vulnerabilities.php

See INSTALL file for build instructions.
More info can be found on-line at http://wolfssl.com/wolfSSL/Docs.html


# wolfSSL (Formerly CyaSSL) Release 3.9.10 (9/23/2016)

## Release 3.9.10 of wolfSSL has bug fixes and new features including:

- Default configure option changes:
  1. DES3 disabled by default
  2. ECC Supported Curves Extension enabled by default
  3. New option Extended Master Secret enabled by default
- Added checking CA certificate path length, and new test certs
- Fix to DSA pre padding and sanity check on R/S values
- Added CTX level RNG for single-threaded builds
- Intel RDSEED enhancements
- ARMv8 hardware acceleration support for AES-CBC/CTR/GCM, SHA-256
- Arduino support updates
- Added the Extended Master Secret TLS extension
  1. Enabled by default in configure options, API to disable
  2. Added support for Extended Master Secret to sniffer
- OCSP fix with issuer key hash, lookup refactor
- Added support for Frosted OS
- Added support for DTLS over SCTP
- Added support for static memory with wolfCrypt
- Fix to ECC Custom Curve support
- Support for asynchronous wolfCrypt RSA and TLS client
- Added distribution build configure option
- Update the test certificates

This release of wolfSSL fixes medium level security vulnerabilities.  Fixes for
potential AES, RSA, and ECC side channel leaks is included that a local user
monitoring the same CPU core cache could exploit.  VM users, hyper-threading
users, and users where potential attackers have access to the CPU cache will
need to update if they utilize AES, RSA private keys, or ECC private keys.
Thanks to Gorka Irazoqui Apecechea and Xiaofei Guo from Intel Corporation for
the report.  More information will be available on our site:

https://wolfssl.com/wolfSSL/security/vulnerabilities.php

See INSTALL file for build instructions.
More info can be found on-line at https://wolfssl.com/wolfSSL/Docs.html


# wolfSSL (Formerly CyaSSL) Release 3.9.8 (7/29/2016)

##Release 3.9.8 of wolfSSL has bug fixes and new features including:

- Add support for custom ECC curves.
- Add cipher suite ECDHE-ECDSA-AES128-CCM.
- Add compkey enable option. This option is for compressed ECC keys.
- Add in the option to use test.h without gettimeofday function using the macro
  WOLFSSL_USER_CURRTIME.
- Add RSA blinding for private key operations. Enable option of harden which is
  on by default. This negates timing attacks.
- Add ECC and TLS support for all SECP, Koblitz and Brainpool curves.
- Add helper functions for static memory option to allow getting optimum buffer
  sizes.
- Update DTLS behavior on bad MAC. DTLS silently drops packets with bad MACs now.
- Update fp_isprime function from libtom enchancement/cleanup repository.
- Update sanity checks on inputs and return values for AES-CMAC.
- Update wolfSSL for use with MYSQL v5.6.30.
- Update LPCXpresso eclipse project to not include misc.c when not needed.
- Fix retransmit of last DTLS flight with timeout notification. The last flight
  is no longer retransmitted on timeout.
- Fixes to some code in math sections for compressed ECC keys. This includes
  edge cases for buffer size on allocation and adjustments for compressed curves
  build. The code and full list can be found on github with pull request #456.
- Fix function argument mismatch for build with secure renegotiation.
- X.509 bug fixes for reading in malformed certificates, reported by researchers
  at Columbia University
- Fix GCC version 6 warning about hard tabs in poly1305.c. This was a warning
  produced by GCC 6 trying to determine the intent of code.
- Fixes for static memory option. Including avoid potential race conditions with
  counters, decrement handshake counter correctly.
- Fix anonymous cipher with Diffie Hellman on the server side. Was an issue of a
  possible buffer corruption. For information and code see pull request #481.


- One high level security fix that requires an update for use with static RSA
  cipher suites was submitted. This fix was the addition of RSA blinding for
  private RSA operations. We recommend servers who allow static RSA cipher
  suites to also generate new private RSA keys. Static RSA cipher suites are
  turned off by default.

See INSTALL file for build instructions.
More info can be found on-line at //http://wolfssl.com/wolfSSL/Docs.html

# wolfSSL (Formerly CyaSSL) Release 3.9.6 (6/14/2016)

##Release 3.9.6 of wolfSSL has bug fixes and new features including:

- Add staticmemory feature
- Add public wc_GetTime API with base64encode feature
- Add AES CMAC algorithm
- Add DTLS sessionexport feature
- Add python wolfCrypt wrapper
- Add ECC encrypt/decrypt benchmarks
- Add dynamic session tickets
- Add eccshamir option
- Add Whitewood netRandom support --with-wnr
- Add embOS port
- Add minimum key size checks for RSA and ECC
- Add STARTTLS support to examples
- Add uTasker port
- Add asynchronous crypto and wolf event support
- Add compile check for misc.c with inline
- Add RNG benchmark
- Add reduction to stack usage with hash-based RNG
- Update STM32F2_CRYPTO port with additional algorithms supported
- Update MDK5 projects
- Update AES-NI
- Fix for STM32 with STM32F2_HASH defined
- Fix for building with MinGw
- Fix ECC math bugs with ALT_ECC_SIZE and key sizes over 256 bit (1)
- Fix certificate buffers github issue #422
- Fix decrypt max size with RSA OAEP
- Fix DTLS sanity check with DTLS timeout notification
- Fix free of WOLFSSL_METHOD on failure to create CTX
- Fix memory leak in failure case with wc_RsaFunction (2)

- No high level security fixes that requires an update though we always
recommend updating to the latest
- (1) Code changes for ECC fix can be found at pull requests #411, #416, and #428
- (2) Builds using RSA with using normal math and not RSA_LOW_MEM should update

See INSTALL file for build instructions.
More info can be found on-line at //http://wolfssl.com/wolfSSL/Docs.html

# wolfSSL (Formerly CyaSSL) Release 3.9.0 (03/18/2016)

##Release 3.9.0 of wolfSSL has bug fixes and new features including:

- Add new leantls configuration
- Add RSA OAEP padding at wolfCrypt level
- Add Arduino port and example client
- Add fixed point DH operation
- Add CUSTOM_RAND_GENRATE_SEED_OS and CUSTOM_RAND_GENERATE_BLOCK
- Add ECDHE-PSK cipher suites
- Add PSK ChaCha20-Poly1305 cipher suites
- Add option for fail on no peer cert except PSK suites
- Add port for Nordic nRF51
- Add additional ECC NIST test vectors for 256, 384 and 521
- Add more granular ECC, Ed25519/Curve25519 and AES configs
- Update to ChaCha20-Poly1305
- Update support for Freescale KSDK 1.3.0
- Update DER buffer handling code, refactoring and reducing memory
- Fix to AESNI 192 bit key expansion
- Fix to C# wrapper character encoding
- Fix sequence number issue with DTLS epoch 0 messages
- Fix RNGA with K64 build
- Fix ASN.1 X509 V3 certificate policy extension parsing
- Fix potential free of uninitialized RSA key in asn.c
- Fix potential underflow when using ECC build with FP_ECC
- Fixes for warnings in Visual Studio 2015 build

- No high level security fixes that requires an update though we always
recommend updating to the latest
- FP_ECC is off by default, users with it enabled should update for the zero
sized hash fix

See INSTALL file for build instructions.
More info can be found on-line at //http://wolfssl.com/yaSSL/Docs.html

# wolfSSL (Formerly CyaSSL) Release 3.8.0 (12/30/2015)

##Release 3.8.0 of wolfSSL has bug fixes and new features including:

- Example client/server with VxWorks
- AESNI use with AES-GCM
- Stunnel compatibility enhancements
- Single shot hash and signature/verify API added
- Update cavium nitrox port
- LPCXpresso IDE support added
- C# wrapper to support wolfSSL use by a C# program
- (BETA version)OCSP stapling added
- Update OpenSSH compatibility
- Improve DTLS handshake when retransmitting finished message
- fix idea_mult() for 16 and 32bit systems
- fix LowResTimer on Microchip ports

- No high level security fixes that requires an update though we always
recommend updating to the latest

See INSTALL file for build instructions.
More info can be found on-line at //http://wolfssl.com/yaSSL/Docs.html

# wolfSSL (Formerly CyaSSL) Release 3.7.0 (10/26/2015)

##Release 3.7.0 of wolfSSL has bug fixes and new features including:

- ALPN extension support added for HTTP2 connections with --enable-alpn
- Change of example/client/client max fragment flag -L -> -F
- Throughput benchmarking, added scripts/benchmark.test
- Sniffer API ssl_FreeDecodeBuffer added
- Addition of AES_GCM to Sniffer
- Sniffer change to handle unlimited decrypt buffer size
- New option for the sniffer where it will try to pick up decoding after a
  sequence number acknowldgement fault. Also includes some additional stats.
- JNI API setter and getter function for jobject added
- User RSA crypto plugin abstraction. An example placed in wolfcrypt/user-crypto
- fix to asn configuration bug
- AES-GCM/CCM fixes.
- Port for Rowley added
- Rowley Crossworks bare metal examples added
- MDK5-ARM project update
- FreeRTOS support updates.
- VXWorks support updates.
- Added the IDEA cipher and support in wolfSSL.
- Update wolfSSL website CA.
- CFLAGS is usable when configuring source.

- No high level security fixes that requires an update though we always
recommend updating to the latest

See INSTALL file for build instructions.
More info can be found on-line at //http://wolfssl.com/yaSSL/Docs.html

#wolfSSL (Formerly CyaSSL) Release 3.6.8 (09/17/2015)

##Release 3.6.8 of wolfSSL fixes two high severity vulnerabilities.
##It also includes bug fixes and new features including:

- Two High level security fixes, all users SHOULD update.
  a) If using wolfSSL for DTLS on the server side of a publicly accessible
     machine you MUST update.
  b) If using wolfSSL for TLS on the server side with private RSA keys allowing
     ephemeral key exchange without low memory optimziations you MUST update and
     regenerate the private RSA keys.

     Please see https://www.wolfssl.com/wolfSSL/Blog/Blog.html for more details

- No filesystem build fixes for various configurations
- Certificate generation now supports several extensions including KeyUsage,
    SKID, AKID, and Ceritifcate Policies
- CRLs can be loaded from buffers as well as files now
- SHA-512 Ceritifcate Signing generation
- Fixes for sniffer reassembly processing

See INSTALL file for build instructions.
More info can be found on-line at //http://wolfssl.com/yaSSL/Docs.html

#wolfSSL (Formerly CyaSSL) Release 3.6.6 (08/20/2015)

##Release 3.6.6 of wolfSSL has bug fixes and new features including:

- OpenSSH  compatibility with --enable-openssh
- stunnel  compatibility with --enable-stunnel
- lighttpd compatibility with --enable-lighty
- SSLv3 is now disabled by default, can be enabled with --enable-sslv3
- Ephemeral key cipher suites only are now supported by default
    To enable static ECDH cipher suites define WOLFSSL_STATIC_DH
    To enable static  RSA cipher suites define WOLFSSL_STATIC_RSA
    To enable static  PSK cipher suites define WOLFSSL_STATIC_PSK
- Added QSH (quantum-safe handshake) extension with --enable-ntru
- SRP is now part of wolfCrypt, enable with --enabe-srp
- Certificate handshake messages can now be sent fragmented if the record
  size is smaller than the total message size, no user action required.
- DTLS duplicate message fixes
- Visual Studio project files now support DLL and static builds for 32/64bit.
- Support for new Freesacle I/O
- FreeRTOS FIPS support

- No high level security fixes that requires an update though we always
  recommend updating to the latest

See INSTALL file for build instructions.
More info can be found on-line at //http://wolfssl.com/yaSSL/Docs.html


#wolfSSL (Formerly CyaSSL) Release 3.6.0 (06/19/2015)

##Release 3.6.0 of wolfSSL has bug fixes and new features including:

- Max Strength build that only allows TLSv1.2, AEAD ciphers, and PFS (Perfect
   Forward Secrecy).  With --enable-maxstrength
- Server side session ticket support, the example server and echosever use the
   example callback myTicketEncCb(), see wolfSSL_CTX_set_TicketEncCb()
- FIPS version submitted for iOS.
- TI Crypto Hardware Acceleration
- DTLS fragmentation fixes
- ECC key check validation with wc_ecc_check_key()
- 32bit code options to reduce memory for Curve25519 and Ed25519
- wolfSSL JNI build switch with --enable-jni
- PicoTCP support improvements
- DH min ephemeral key size enforcement with wolfSSL_CTX_SetMinDhKey_Sz()
- KEEP_PEER_CERT and AltNames can now be used together
- ChaCha20 big endian fix
- SHA-512 signature algorithm support for key exchange and verify messages
- ECC make key crash fix on RNG failure, ECC users must update.
- Improvements to usage of time code.
- Improvements to VS solution files.
- GNU Binutils 2.24 ld has problems with some debug builds, to fix an ld error
  add -fdebug-types-section to C_EXTRA_FLAGS

- No high level security fixes that requires an update though we always
  recommend updating to the latest (except note 14, ecc RNG failure)

See INSTALL file for build instructions.
More info can be found on-line at //http://wolfssl.com/yaSSL/Docs.html


#wolfSSL (Formerly CyaSSL) Release 3.4.8 (04/06/2015)

##Release 3.4.8 of wolfSSL has bug fixes and new features including:

- FIPS version submitted for iOS.
- Max Strength build that only allows TLSv1.2, AEAD ciphers, and PFS.
- Improvements to usage of time code.
- Improvements to VS solution files.

See INSTALL file for build instructions.
More info can be found on-line at //http://wolfssl.com/yaSSL/Docs.html


#wolfSSL (Formerly CyaSSL) Release 3.4.6 (03/30/2015)

##Release 3.4.6 of wolfSSL has bug fixes and new features including:

- Intel Assembly Speedups using instructions rdrand, rdseed, aesni, avx1/2,
  rorx, mulx, adox, adcx .  They can be enabled with --enable-intelasm.
  These speedup the use of RNG, SHA2, and public key algorithms.
- Ed25519 support at the crypto level. Turn on with --enable-ed25519.  Examples
  in wolcrypt/test/test.c ed25519_test().
- Post Handshake Memory reductions.  wolfSSL can now hold less than 1,000 bytes
  of memory per secure connection including cipher state.
- wolfSSL API and wolfCrypt API fixes, you can still include the cyassl and
  ctaocrypt headers which will enable the compatibility APIs for the
  foreseeable future
- INSTALL file to help direct users to build instructions for their environment
- For ECC users with the normal math library a fix that prevents a crash when
  verify signature fails.  Users of 3.4.0 with ECC and the normal math library
  must update
- RC4 is now disabled by default in autoconf mode
- AES-GCM and ChaCha20/Poly1305 are now enabled by default to make AEAD ciphers
  available without a switch
- External ChaCha-Poly AEAD API, thanks to Andrew Burks for the contribution
- DHE-PSK cipher suites can now be built without ASN or Cert support
- Fix some NO MD5 build issues with optional features
- Freescale CodeWarrior project updates
- ECC curves can be individually turned on/off at build time.
- Sniffer handles Cert Status message and other minor fixes
- SetMinVersion() at the wolfSSL Context level instead of just SSL session level
  to allow minimum protocol version allowed at runtime
- RNG failure resource cleanup fix

- No high level security fixes that requires an update though we always
  recommend updating to the latest (except note 6 use case of ecc/normal math)

See INSTALL file for build instructions.
More info can be found on-line at //http://wolfssl.com/yaSSL/Docs.html


#wolfSSL (Formerly CyaSSL) Release 3.4.0 (02/23/2015)

## Release 3.4.0 wolfSSL has bug fixes and new features including:

- wolfSSL API and wolfCrypt API, you can still include the cyassl and ctaocrypt
  headers which will enable the compatibility APIs for the foreseeable future
- Example use of the wolfCrypt API can be found in wolfcrypt/test/test.c
- Example use of the wolfSSL API can be found in examples/client/client.c
- Curve25519 now supported at the wolfCrypt level, wolfSSL layer coming soon
- Improvements in the build configuration under AIX
- Microchip Pic32 MZ updates
- TIRTOS updates
- PowerPC updates
- Xcode project update
- Bidirectional shutdown examples in client/server with -w (wait for full
  shutdown) option
- Cycle counts on benchmarks for x86_64, more coming soon
- ALT_ECC_SIZE for reducing ecc heap use with fastmath when also using large RSA
  keys
- Various compile warnings
- Scan-build warning fixes
- Changed a memcpy to memmove in the sniffer (if using sniffer please update)
- No high level security fixes that requires an update though we always
  recommend updating to the latest


# CyaSSL Release 3.3.0 (12/05/2014)

- Countermeasuers for Handshake message duplicates, CHANGE CIPHER without
  FINISHED, and fast forward attempts.  Thanks to Karthikeyan Bhargavan from
  the Prosecco team at INRIA Paris-Rocquencourt for the report.
- FIPS version submitted
- Removes SSLv2 Client Hello processing, can be enabled with OLD_HELLO_ALLOWED
- User can set mimimum downgrade version with CyaSSL_SetMinVersion()
- Small stack improvements at TLS/SSL layer
- TLS Master Secret generation and Key Expansion are now exposed
- Adds client side Secure Renegotiation, * not recommended *
- Client side session ticket support, not fully tested with Secure Renegotiation
- Allows up to 4096bit DHE at TLS Key Exchange layer
- Handles non standard SessionID sizes in Hello Messages
- PicoTCP Support
- Sniffer now supports SNI Virtual Hosts
- Sniffer now handles non HTTPS protocols using STARTTLS
- Sniffer can now parse records with multiple messages
- TI-RTOS updates
- Fix for ColdFire optimized fp_digit read only in explicit 32bit case
- ADH Cipher Suite ADH-AES128-SHA for EAP-FAST

The CyaSSL manual is available at:
http://www.wolfssl.com/documentation/CyaSSL-Manual.pdf.  For build instructions
and comments about the new features please check the manual.


# CyaSSL Release 3.2.0 (09/10/2014)

#### Release 3.2.0 CyaSSL has bug fixes and new features including:

- ChaCha20 and Poly1305 crypto and suites
- Small stack improvements for OCSP, CRL, TLS, DTLS
- NTRU Encrypt and Decrypt benchmarks
- Updated Visual Studio project files
- Updated Keil MDK5 project files
- Fix for DTLS sequence numbers with GCM/CCM
- Updated HashDRBG with more secure struct declaration
- TI-RTOS support and example Code Composer Studio project files
- Ability to get enabled cipher suites, CyaSSL_get_ciphers()
- AES-GCM/CCM/Direct support for Freescale mmCAU and CAU
- Sniffer improvement checking for decrypt key setup
- Support for raw ECC key import
- Ability to convert ecc_key to DER, EccKeyToDer()
- Security fix for RSA Padding check vulnerability reported by Intel Security
  Advanced Threat Research team

The CyaSSL manual is available at:
http://www.wolfssl.com/documentation/CyaSSL-Manual.pdf.  For build instructions
and comments about the new features please check the manual.


# CyaSSL Release 3.1.0 (07/14/2014)

#### Release 3.1.0 CyaSSL has bug fixes and new features including:

- Fix for older versions of icc without 128-bit type
- Intel ASM syntax for AES-NI
- Updated NTRU support, keygen benchmark
- FIPS check for minimum required HMAC key length
- Small stack (--enable-smallstack) improvements for PKCS#7, ASN
- TLS extension support for DTLS
- Default I/O callbacks external to user
- Updated example client with bad clock test
- Ability to set optional ECC context info
- Ability to enable/disable DH separate from opensslextra
- Additional test key/cert buffers for CA and server
- Updated example certificates

The CyaSSL manual is available at:
http://www.yassl.com/documentation/CyaSSL-Manual.pdf.  For build instructions
and comments about the new features please check the manual.


# CyaSSL Release 3.0.2 (05/30/2014)

#### Release 3.0.2 CyaSSL has bug fixes and new features including:

- Added the following cipher suites:
  * TLS_PSK_WITH_AES_128_GCM_SHA256
  * TLS_PSK_WITH_AES_256_GCM_SHA384
  * TLS_PSK_WITH_AES_256_CBC_SHA384
  * TLS_PSK_WITH_NULL_SHA384
  * TLS_DHE_PSK_WITH_AES_128_GCM_SHA256
  * TLS_DHE_PSK_WITH_AES_256_GCM_SHA384
  * TLS_DHE_PSK_WITH_AES_128_CBC_SHA256
  * TLS_DHE_PSK_WITH_AES_256_CBC_SHA384
  * TLS_DHE_PSK_WITH_NULL_SHA256
  * TLS_DHE_PSK_WITH_NULL_SHA384
  * TLS_DHE_PSK_WITH_AES_128_CCM
  * TLS_DHE_PSK_WITH_AES_256_CCM
- Added AES-NI support for Microsoft Visual Studio builds.
- Changed small stack build to be disabled by default.
- Updated the Hash DRBG and provided a configure option to enable.

The CyaSSL manual is available at:
http://www.yassl.com/documentation/CyaSSL-Manual.pdf.  For build instructions
and comments about the new features please check the manual.


# CyaSSL Release 3.0.0 (04/29/2014)

#### Release 3.0.0 CyaSSL has bug fixes and new features including:

- FIPS release candidate
- X.509 improvements that address items reported by Suman Jana with security
  researchers at UT Austin and UC Davis
- Small stack size improvements, --enable-smallstack. Offloads large local
  variables to the heap. (Note this is not complete.)
- Updated AES-CCM-8 cipher suites to use approved suite numbers.

The CyaSSL manual is available at:
http://www.yassl.com/documentation/CyaSSL-Manual.pdf.  For build instructions
and comments about the new features please check the manual.


# CyaSSL Release 2.9.4 (04/09/2014)

#### Release 2.9.4 CyaSSL has bug fixes and new features including:

- Security fixes that address items reported by Ivan Fratric of the Google
  Security Team
- X.509 Unknown critical extensions treated as errors, report by Suman Jana with
  security researchers at UT Austin and UC Davis
- Sniffer fixes for corrupted packet length and Jumbo frames
- ARM thumb mode assembly fixes
- Xcode 5.1 support including new clang
- PIC32 MZ hardware support
- CyaSSL Object has enough room to read the Record Header now w/o allocs
- FIPS wrappers for AES, 3DES, SHA1, SHA256, SHA384, HMAC, and RSA.
- A sample I/O pool is demonstrated with --enable-iopool to overtake memory
  handling and reduce memory fragmentation on I/O large sizes

The CyaSSL manual is available at:
http://www.yassl.com/documentation/CyaSSL-Manual.pdf.  For build instructions 
and comments about the new features please check the manual.


# CyaSSL Release 2.9.0 (02/07/2014)

#### Release 2.9.0 CyaSSL has bug fixes and new features including:
- Freescale Kinetis RNGB support
- Freescale Kinetis mmCAU support
- TLS Hello extensions
  - ECC
  - Secure Renegotiation (null) 
  - Truncated HMAC
- SCEP support
  - PKCS #7 Enveloped data and signed data
  - PKCS #10 Certificate Signing Request generation
- DTLS sliding window
- OCSP Improvements
  - API change to integrate into Certificate Manager
  - IPv4/IPv6 agnostic
  - example client/server support for OCSP
  - OCSP nonces are optional
- GMAC hashing
- Windows build additions
- Windows CYGWIN build fixes
- Updated test certificates
- Microchip MPLAB Harmony support
- Update autoconf scripts
- Additional X.509 inspection functions
- ECC encrypt/decrypt primitives
- ECC Certificate generation

The Freescale Kinetis K53 RNGB documentation can be found in Chapter 33 of the
K53 Sub-Family Reference Manual:
http://cache.freescale.com/files/32bit/doc/ref_manual/K53P144M100SF2RM.pdf

Freescale Kinetis K60 mmCAU (AES, DES, 3DES, MD5, SHA, SHA256) documentation
can be found in the "ColdFire/ColdFire+ CAU and Kinetis mmCAU Software Library
User Guide":
http://cache.freescale.com/files/32bit/doc/user_guide/CAUAPIUG.pdf


# CyaSSL Release 2.8.0 (8/30/2013)

#### Release 2.8.0 CyaSSL has bug fixes and new features including:
- AES-GCM and AES-CCM use AES-NI
- NetX default IO callback handlers
- IPv6 fixes for DTLS Hello Cookies
- The ability to unload Certs/Keys after the handshake, CyaSSL_UnloadCertsKeys()
- SEP certificate extensions
- Callback getters for easier resource freeing
- External CYASSL_MAX_ERROR_SZ for correct error buffer sizing
- MacEncrypt and DecryptVerify Callbacks for User Atomic Record Layer Processing
- Public Key Callbacks for ECC and RSA
- Client now sends blank cert upon request if doesn't have one with TLS <= 1.2


The CyaSSL manual is available at:
http://www.yassl.com/documentation/CyaSSL-Manual.pdf.  For build instructions 
and comments about the new features please check the manual.


# CyaSSL Release 2.7.0 (6/17/2013)

#### Release 2.7.0 CyaSSL has bug fixes and new features including:
- SNI support for client and server
- KEIL MDK-ARM projects
- Wildcard check to domain name match, and Subject altnames are checked too
- Better error messages for certificate verification errors
- Ability to discard session during handshake verify
- More consistent error returns across all APIs
- Ability to unload CAs at the CTX or CertManager level
- Authority subject id support for Certificate matching
- Persistent session cache functionality
- Persistent CA cache functionality
- Client session table lookups to push serverID table to library level
- Camellia support to sniffer
- User controllable settings for DTLS timeout values
- Sniffer fixes for caching long lived sessions
- DTLS reliability enhancements for the handshake
- Better ThreadX support

When compiling with Mingw, libtool may give the following warning due to
path conversion errors:
 
```
libtool: link: Could not determine host file name corresponding to **
libtool: link: Continuing, but uninstalled executables may not work.
```

If so, examples and testsuite will have problems when run, showing an
error while loading shared libraries. To resolve, please run "make install".

The CyaSSL manual is available at:
http://www.yassl.com/documentation/CyaSSL-Manual.pdf.  For build instructions 
and comments about the new features please check the manual.


# CyaSSL Release 2.6.0 (04/15/2013)

#### Release 2.6.0 CyaSSL has bug fixes and new features including:
- DTLS 1.2 support including AEAD ciphers
- SHA-3 finalist Blake2 support, it's fast and uses little resources
- SHA-384 cipher suites including ECC ones
- HMAC now supports SHA-512
- Track memory use for example client/server with -t option
- Better IPv6 examples with --enable-ipv6, before if ipv6 examples/tests were
  turned on, localhost only was used.  Now link-local (with scope ids) and ipv6
  hosts can be used as well.
- Xcode v4.6 project for iOS v6.1 update
- settings.h is now checked in all *.c files for true one file setting detection
- Better alignment at SSL layer for hardware crypto alignment needs
    * Note, SSL itself isn't friendly to alignment with 5 byte TLS headers and
      13 bytes DTLS headers, but every effort is now made to align with the
      CYASSL_GENERAL_ALIGNMENT flag which sets desired alignment requirement
- NO_64BIT flag to turn off 64bit data type accumulators in public key code
    * Note, some systems are faster with 32bit accumulators 
- --enable-stacksize for example client/server stack use
    * Note, modern desktop Operating Systems may add bytes to each stack frame
- Updated compression/decompression with direct crypto access
- All ./configure options are now lowercase only for consistency
- ./configure builds default to fastmath option
    * Note, if on ia32 and building in shared mode this may produce a problem
      with a missing register being available because of PIC, there are at least
      6 solutions to this:
      1) --disable-fastmath , don't use fastmath
      2) --disable-shared, don't build a shared library
      3) C_EXTRA_FLAGS=-DTFM_NO_ASM , turn off assembly use
      4) use clang, it just seems to work
      5) play around with no PIC options to force all registers being open,
         e.g., --without-pic
      6) if static lib is still a problem try removing fPIE
- Many new ./configure switches for option enable/disable for example
    * rsa
    * dh
    * dsa
    * md5
    * sha 
    * arc4
    * null    (allow NULL ciphers)
    * oldtls  (only use TLS 1.2)
    * asn     (no certs or public keys allowed)
- ./configure generates cyassl/options.h which allows a header the user can 
  include in their app to make sure the same options are set at the app and
  CyaSSL level.
- autoconf no longer needs serial-tests which lowers version requirements of
  automake to 1.11 and autoconf to 2.63

The CyaSSL manual is available at:
http://www.yassl.com/documentation/CyaSSL-Manual.pdf.  For build instructions 
and comments about the new features please check the manual.



# CyaSSL Release 2.5.0 (02/04/2013)

#### Release 2.5.0 CyaSSL has bug fixes and new features including:
- Fix for TLS CBC padding timing attack identified by Nadhem Alfardan and
  Kenny Paterson: http://www.isg.rhul.ac.uk/tls/
- Microchip PIC32 (MIPS16, MIPS32) support
- Microchip MPLAB X example projects for PIC32 Ethernet Starter Kit
- Updated CTaoCrypt benchmark app for embedded systems
- 1024-bit test certs/keys and cert/key buffers
- AES-CCM-8 crypto and cipher suites
- Camellia crypto and cipher suites
- Bumped minimum autoconf version to 2.65, automake version to 1.12
- Addition of OCSP callbacks
- STM32F2 support with hardware crypto and RNG 
- Cavium NITROX support

CTaoCrypt now has support for the Microchip PIC32 and has been tested with
the Microchip PIC32 Ethernet Starter Kit, the XC32 compiler and
MPLAB X IDE in both MIPS16 and MIPS32 instruction set modes. See the README
located under the <cyassl_root>/mplabx directory for more details.

To add Cavium NITROX support do:

./configure --with-cavium=/home/user/cavium/software

pointing to your licensed cavium/software directory.  Since Cavium doesn't
build a library we pull in the cavium_common.o file which gives a libtool 
warning about the portability of this.  Also, if you're using the github source
tree you'll need to remove the -Wredundant-decls warning from the generated
Makefile because the cavium headers don't conform to this warning.  Currently
CyaSSL supports Cavium RNG, AES, 3DES, RC4, HMAC, and RSA directly at the crypto
layer.  Support at the SSL level is partial and currently just does AES, 3DES,
and RC4.  RSA and HMAC are slower until the Cavium calls can be utilized in non
blocking mode.  The example client turns on cavium support as does the crypto
test and benchmark.  Please see the HAVE_CAVIUM define.

CyaSSL is able to use the STM32F2 hardware-based cryptography and random number
generator through the STM32F2 Standard Peripheral Library. For necessary
defines, see the CYASSL_STM32F2 define in settings.h. Documentation for the
STM32F2 Standard Peripheral Library can be found in the following document: 
http://www.st.com/internet/com/TECHNICAL_RESOURCES/TECHNICAL_LITERATURE/USER_MANUAL/DM00023896.pdf

The CyaSSL manual is available at:
http://www.yassl.com/documentation/CyaSSL-Manual.pdf.  For build instructions 
and comments about the new features please check the manual.



# CyaSSL Release 2.4.6 (12/20/2012)

#### Release 2.4.6 CyaSSL has bug fixes and a few new features including:
- ECC into main version
- Lean PSK build (reduced code size, RAM usage, and stack usage)
- FreeBSD CRL monitor support
- CyaSSL_peek()
- CyaSSL_send() and CyaSSL_recv() for I/O flag setting
- CodeWarrior Support
- MQX Support
- Freescale Kinetis support including Hardware RNG
- autoconf builds use jobserver
- cyassl-config
- Sniffer memory reductions

Thanks to Brian Aker for the improved autoconf system, make rpm, cyassl-config,
warning system, and general good ideas for improving CyaSSL!

The Freescale Kinetis K70 RNGA documentation can be found in Chapter 37 of the
K70 Sub-Family Reference Manual:
http://cache.freescale.com/files/microcontrollers/doc/ref_manual/K70P256M150SF3RM.pdf

The CyaSSL manual is available at:
http://www.yassl.com/documentation/CyaSSL-Manual.pdf.  For build instructions 
and comments about the new features please check the manual.


# CyaSSL Release 2.4.0 (10/10/2012)

#### Release 2.4.0 CyaSSL has bug fixes and a few new features including:
- DTLS reliability
- Reduced memory usage after handshake
- Updated build process

The CyaSSL manual is available at:
http://www.yassl.com/documentation/CyaSSL-Manual.pdf.  For build instructions 
and comments about the new features please check the manual.



# CyaSSL Release 2.3.0 (8/10/2012)

#### Release 2.3.0 CyaSSL has bug fixes and a few new features including:
- AES-GCM crypto and cipher suites
- make test cipher suite checks
- Subject AltName processing
- Command line support for client/server examples
- Sniffer SessionTicket support
- SHA-384 cipher suites
- Verify cipher suite validity when user overrides
- CRL dir monitoring
- DTLS Cookie support, reliability coming soon

The CyaSSL manual is available at:
http://www.yassl.com/documentation/CyaSSL-Manual.pdf.  For build instructions 
and comments about the new features please check the manual.



# CyaSSL Release 2.2.0 (5/18/2012)

#### Release 2.2.0 CyaSSL has bug fixes and a few new features including:
- Initial CRL support (--enable-crl)
- Initial OCSP support (--enable-ocsp)
- Add static ECDH suites
- SHA-384 support
- ECC client certificate support
- Add medium session cache size (1055 sessions) 
- Updated unit tests
- Protection against mutex reinitialization


The CyaSSL manual is available at:
http://www.yassl.com/documentation/CyaSSL-Manual.pdf.  For build instructions 
and comments about the new features please check the manual.



# CyaSSL Release 2.0.8 (2/24/2012)

#### Release 2.0.8 CyaSSL has bug fixes and a few new features including:
- A fix for malicious certificates pointed out by Remi Gacogne (thanks)
  resulting in NULL pointer use.
- Respond to renegotiation attempt with no_renegoatation alert
- Add basic path support for load_verify_locations()
- Add set Temp EC-DHE key size
- Extra checks on rsa test when porting into


The CyaSSL manual is available at:
http://www.yassl.com/documentation/CyaSSL-Manual.pdf.  For build instructions 
and comments about the new features please check the manual.



# CyaSSL Release 2.0.6 (1/27/2012)

#### Release 2.0.6 CyaSSL has bug fixes and a few new features including:
- Fixes for CA basis constraint check
- CTX reference counting
- Initial unit test additions
- Lean and Mean Windows fix
- ECC benchmarking
- SSMTP build support
- Ability to group handshake messages with set_group_messages(ctx/ssl)
- CA cache addition callback
- Export Base64_Encode for general use

The CyaSSL manual is available at:
http://www.yassl.com/documentation/CyaSSL-Manual.pdf.  For build instructions 
and comments about the new features please check the manual.



# CyaSSL Release 2.0.2 (12/05/2011)

#### Release 2.0.2 CyaSSL has bug fixes and a few new features including:
- CTaoCrypt Runtime library detection settings when directly using the crypto
  library
- Default certificate generation now uses SHAwRSA and adds SHA256wRSA generation
- All test certificates now use 2048bit and SHA-1 for better modern browser
  support
- Direct AES block access and AES-CTR (counter) mode
- Microchip pic32 support

The CyaSSL manual is available at:
http://www.yassl.com/documentation/CyaSSL-Manual.pdf.  For build instructions 
and comments about the new features please check the manual.



# CyaSSL Release 2.0.0rc3 (9/28/2011)

#### Release 2.0.0rc3 for CyaSSL has bug fixes and a few new features including:
- updated autoconf support
- better make install and uninstall  (uses system directories)
- make test / make check
- CyaSSL headers now in <cyassl/*.h>
- CTaocrypt headers now in <cyassl/ctaocrypt/*.h>
- OpenSSL compatibility headers now in <cyassl/openssl/*.h>
- examples and tests all run from home directory so can use certs in ./certs
        (see note 1)

So previous applications that used the OpenSSL compatibility header
<openssl/ssl.h> now need to include <cyassl/openssl/ssl.h> instead, no other
changes are required.

Special Thanks to Brian Aker for his autoconf, install, and header patches.

The CyaSSL manual is available at:
http://www.yassl.com/documentation/CyaSSL-Manual.pdf.  For build instructions 
and comments about the new features please check the manual.

# CyaSSL Release 2.0.0rc2 (6/6/2011)

#### Release 2.0.0rc2 for CyaSSL has bug fixes and a few new features including:
- bug fixes (Alerts, DTLS with DHE)
- FreeRTOS support
- lwIP support
- Wshadow warnings removed
- asn public header
- CTaoCrypt public headers now all have ctc_ prefix (the manual is still being
        updated to reflect this change)
- and more.

This is the 2nd and perhaps final release candidate for version 2.
Please send any comments or questions to support@yassl.com.

The CyaSSL manual is available at:
http://www.yassl.com/documentation/CyaSSL-Manual.pdf.  For build instructions 
and comments about the new features please check the manual.

# CyaSSL Release 2.0.0rc1 (5/2/2011)

#### Release 2.0.0rc1 for CyaSSL has many new features including:
- bug fixes
- SHA-256 cipher suites 
- Root Certificate Verification (instead of needing all certs in the chain) 
- PKCS #8 private key encryption (supports PKCS #5 v1-v2 and PKCS #12) 
- Serial number retrieval for x509 
- PBKDF2 and PKCS #12 PBKDF 
- UID parsing for x509 
- SHA-256 certificate signatures 
- Client and server can send chains (SSL_CTX_use_certificate_chain_file) 
- CA loading can now parse multiple certificates per file
- Dynamic memory runtime hooks
- Runtime hooks for logging
- EDH on server side
- More informative error codes
- More informative logging messages
- Version downgrade more robust (use SSL_v23*)
- Shared build only by default through ./configure
- Compiler visibility is now used, internal functions not polluting namespace
- Single Makefile, no recursion, for faster and simpler building
- Turn on all warnings possible build option, warning fixes
- and more.

Because of all the new features and the multiple OS, compiler, feature-set
options that CyaSSL allows, there may be some configuration fixes needed.
Please send any comments or questions to support@yassl.com.

The CyaSSL manual is available at:
http://www.yassl.com/documentation/CyaSSL-Manual.pdf.  For build instructions 
and comments about the new features please check the manual.

# CyaSSL Release 1.9.0 (3/2/2011)

Release 1.9.0 for CyaSSL adds bug fixes, improved TLSv1.2 through testing and
better hash/sig algo ids, --enable-webServer for the yaSSL embedded web server,
improper AES key setup detection, user cert verify callback improvements, and
more.

The CyaSSL manual offering is included in the doc/ directory.  For build
instructions and comments about the new features please check the manual.

Please send any comments or questions to support@yassl.com.

# CyaSSL Release 1.8.0 (12/23/2010)

Release 1.8.0 for CyaSSL adds bug fixes, x509 v3 CA signed certificate
generation, a C standard library abstraction layer, lower memory use, increased
portability through the os_settings.h file, and the ability to use NTRU cipher
suites when used in conjunction with an NTRU license and library.

The initial CyaSSL manual offering is included in the doc/ directory.  For
build instructions and comments about the new features please check the manual.

Please send any comments or questions to support@yassl.com.

Happy Holidays.
 

# CyaSSL Release 1.6.5 (9/9/2010)

Release 1.6.5 for CyaSSL adds bug fixes and x509 v3 self signed certificate
generation.
 
For general build instructions see doc/Building_CyaSSL.pdf.

To enable certificate generation support add this option to ./configure
./configure --enable-certgen

An example is included in ctaocrypt/test/test.c and documentation is provided
in doc/CyaSSL_Extensions_Reference.pdf item 11.

# CyaSSL Release 1.6.0 (8/27/2010)

Release 1.6.0 for CyaSSL adds bug fixes, RIPEMD-160, SHA-512, and RSA key
generation.
 
For general build instructions see doc/Building_CyaSSL.pdf.

To add RIPEMD-160 support add this option to ./configure
./configure --enable-ripemd

To add SHA-512 support add this option to ./configure
./configure --enable-sha512

To add RSA key generation support add this option to ./configure
./configure --enable-keygen

Please see ctaocrypt/test/test.c for examples and usage.

For Windows, RIPEMD-160 and SHA-512 are enabled by default but key generation is
off by default.  To turn key generation on add the define CYASSL_KEY_GEN to
CyaSSL.


# CyaSSL Release 1.5.6 (7/28/2010)

Release 1.5.6 for CyaSSL adds bug fixes, compatibility for our JSSE provider,
and a fix for GCC builds on some systems.
 
For general build instructions see doc/Building_CyaSSL.pdf.

To add AES-NI support add this option to ./configure
./configure --enable-aesni

You'll need GCC 4.4.3 or later to make use of the assembly.

# CyaSSL Release 1.5.4 (7/7/2010)

Release 1.5.4 for CyaSSL adds bug fixes, support for AES-NI, SHA1 speed 
improvements from loop unrolling, and support for the Mongoose Web Server.
 
For general build instructions see doc/Building_CyaSSL.pdf.

To add AES-NI support add this option to ./configure
./configure --enable-aesni

You'll need GCC 4.4.3 or later to make use of the assembly.

# CyaSSL Release 1.5.0 (5/11/2010)

Release 1.5.0 for CyaSSL adds bug fixes, GoAhead WebServer support, sniffer
support, and initial swig interface support.

For general build instructions see doc/Building_CyaSSL.pdf.

To add support for GoAhead WebServer either --enable-opensslExtra or if you
don't want all the features of opensslExtra you can just define GOAHEAD_WS
instead.  GOAHEAD_WS can be added to ./configure with CFLAGS=-DGOAHEAD_WS or
you can define it yourself.

To look at the sniffer support please see the sniffertest app in
sslSniffer/sslSnifferTest.  Build with --enable-sniffer on *nix or use the
vcproj files on windows.  You'll need to have pcap installed on *nix and
WinPcap on windows.

A swig interface file is now located in the swig directory for using Python,
Java, Perl, and others with CyaSSL.  This is initial support and experimental,
please send questions or comments to support@yassl.com.

When doing load testing with CyaSSL, on the echoserver example say, the client
machine may run out of tcp ephemeral ports, they will end up in the TIME_WAIT
queue, and can't be reused by default.  There are generally two ways to fix
this. 

1. Reduce the length sockets remain on the TIME_WAIT queue OR
2. Allow items on the TIME_WAIT queue to be reused.


To reduce the TIME_WAIT length in OS X to 3 seconds (3000 milliseconds)

`sudo sysctl -w net.inet.tcp.msl=3000`

In Linux

`sudo sysctl -w net.ipv4.tcp_tw_reuse=1`

allows reuse of sockets in TIME_WAIT

`sudo sysctl -w net.ipv4.tcp_tw_recycle=1`

works but seems to remove sockets from  TIME_WAIT entirely?

`sudo sysctl -w net.ipv4.tcp_fin_timeout=1`

doen't control TIME_WAIT, it controls FIN_WAIT(2) contrary to some posts


# CyaSSL Release 1.4.0 (2/18/2010)

Release 1.3.0 for CyaSSL adds bug fixes, better multi TLS/SSL version support
through SSLv23_server_method(), and improved documentation in the doc/ folder.

For general build instructions doc/Building_CyaSSL.pdf.

# CyaSSL Release 1.3.0 (1/21/2010)

Release 1.3.0 for CyaSSL adds bug fixes, a potential security problem fix,
better porting support, removal of assert()s, and a complete THREADX port.

For general build instructions see rc1 below.

# CyaSSL Release 1.2.0 (11/2/2009)

Release 1.2.0 for CyaSSL adds bug fixes and session negotiation if first use is
read or write.

For general build instructions see rc1 below.

# CyaSSL Release 1.1.0 (9/2/2009)

Release 1.1.0 for CyaSSL adds bug fixes, a check against malicious session
cache use, support for lighttpd, and TLS 1.2.

To get TLS 1.2 support please use the client and server functions:

```c
SSL_METHOD *TLSv1_2_server_method(void);
SSL_METHOD *TLSv1_2_client_method(void);
```

CyaSSL was tested against lighttpd 1.4.23.  To build CyaSSL for use with 
lighttpd use the following commands from the CyaSSL install dir <CyaSSLDir>:

```
./configure --disable-shared --enable-opensslExtra --enable-fastmath --without-zlib

make
make openssl-links
```

Then to build lighttpd with CyaSSL use the following commands from the
lighttpd install dir:

```
./configure --with-openssl --with-openssl-includes=<CyaSSLDir>/include --with-openssl-libs=<CyaSSLDir>/lib LDFLAGS=-lm

make
```

On some systems you may get a linker error about a duplicate symbol for
MD5_Init or other MD5 calls.  This seems to be caused by the lighttpd src file
md5.c, which defines MD5_Init(), and is included in liblightcomp_la-md5.o.
When liblightcomp is linked with the SSL_LIBs the linker may complain about
the duplicate symbol.  This can be fixed by editing the lighttpd src file md5.c
and adding this line to the beginning of the file:

\#if 0

and this line to the end of the file

\#endif

Then from the lighttpd src dir do a:

```
make clean
make
```

If you get link errors about undefined symbols more than likely the actual
OpenSSL libraries are found by the linker before the CyaSSL openssl-links that
point to the CyaSSL library, causing the linker confusion.  This can be fixed
by editing the Makefile in the lighttpd src directory and changing the line:

`SSL_LIB = -lssl -lcrypto`

to

`SSL_LIB = -lcyassl`

Then from the lighttpd src dir do a:

```
make clean
make
```

This should remove any confusion the linker may be having with missing symbols.

For any questions or concerns please contact support@yassl.com .

For general build instructions see rc1 below.

# CyaSSL Release 1.0.6 (8/03/2009)

Release 1.0.6 for CyaSSL adds bug fixes, an improved session cache, and faster
math with a huge code option.

The session cache now defaults to a client mode, also good for embedded servers.
For servers not under heavy load (less than 200 new sessions per minute), define
BIG_SESSION_CACHE.  If the server will be under heavy load, define
HUGE_SESSION_CACHE.

There is now a fasthugemath option for configure.  This enables fastmath plus
even faster math by greatly increasing the code size of the math library. Use
the benchmark utility to compare public key operations.


For general build instructions see rc1 below.

# CyaSSL Release 1.0.3 (5/10/2009)

Release 1.0.3 for CyaSSL adds bug fixes and add increased support for OpenSSL
compatibility when building other applications.

Release 1.0.3 includes an alpha release of DTLS for both client and servers.
This is only for testing purposes at this time.  Rebroadcast and reordering
aren't fully implemented at this time but will be for the next release.

For general build instructions see rc1 below.

# CyaSSL Release 1.0.2 (4/3/2009)

Release 1.0.2 for CyaSSL adds bug fixes for a couple I/O issues.  Some systems
will send a SIGPIPE on socket recv() at any time and this should be handled by
the application by turning off SIGPIPE through setsockopt() or returning from
the handler.

Release 1.0.2 includes an alpha release of DTLS for both client and servers.
This is only for testing purposes at this time.  Rebroadcast and reordering
aren't fully implemented at this time but will be for the next release.

For general build instructions see rc1 below.

## CyaSSL Release Candidate 3 rc3-1.0.0 (2/25/2009)


Release Candidate 3 for CyaSSL 1.0.0 adds bug fixes and adds a project file for
iPhone development with Xcode.  cyassl-iphone.xcodeproj is located in the root
directory.  This release also includes a fix for supporting other
implementations that bundle multiple messages at the record layer, this was
lost when cyassl i/o was re-implemented but is now fixed.

For general build instructions see rc1 below.

## CyaSSL Release Candidate 2 rc2-1.0.0 (1/21/2009)


Release Candidate 2 for CyaSSL 1.0.0 adds bug fixes and adds two new stream
ciphers along with their respective cipher suites.  CyaSSL adds support for
HC-128 and RABBIT stream ciphers.  The new suites are:

```
TLS_RSA_WITH_HC_128_SHA
TLS_RSA_WITH_RABBIT_SHA
```

And the corresponding cipher names are

```
HC128-SHA
RABBIT-SHA
```

CyaSSL also adds support for building with devkitPro for PPC by changing the
library proper to use libogc.  The examples haven't been changed yet but if
there's interest they can be.  Here's an example ./configure to build CyaSSL
for devkitPro:

```
./configure --disable-shared CC=/pathTo/devkitpro/devkitPPC/bin/powerpc-gekko-gcc --host=ppc --without-zlib --enable-singleThreaded RANLIB=/pathTo/devkitpro/devkitPPC/bin/powerpc-gekko-ranlib CFLAGS="-DDEVKITPRO -DGEKKO"
```

For linking purposes you'll need

`LDFLAGS="-g -mrvl -mcpu=750 -meabi -mhard-float -Wl,-Map,$(notdir $@).map"`

For general build instructions see rc1 below.


## CyaSSL Release Candidate 1 rc1-1.0.0 (12/17/2008)


Release Candidate 1 for CyaSSL 1.0.0 contains major internal changes.  Several
areas have optimization improvements, less dynamic memory use, and the I/O
strategy has been refactored to allow alternate I/O handling or Library use.
Many thanks to Thierry Fournier for providing these ideas and most of the work.

Because of these changes, this release is only a candidate since some problems
are probably inevitable on some platform with some I/O use.  Please report any
problems and we'll try to resolve them as soon as possible.  You can contact us
at support@yassl.com or todd@yassl.com.

Using TomsFastMath by passing --enable-fastmath to ./configure now uses assembly
on some platforms.  This is new so please report any problems as every compiler,
mode, OS combination hasn't been tested.  On ia32 all of the registers need to
be available so be sure to pass these options to CFLAGS:

`CFLAGS="-O3 -fomit-frame-pointer"`

OS X will also need -mdynamic-no-pic added to CFLAGS

Also if you're building in shared mode for ia32 you'll need to pass options to
LDFLAGS as well on OS X:

`LDFLAGS=-Wl,-read_only_relocs,warning`

This gives warnings for some symbols but seems to work.


#### To build on Linux, Solaris, *BSD, Mac OS X, or Cygwin:

    ./configure
    make

    from the ./testsuite/ directory run ./testsuite 

#### To make a debug build:

    ./configure --enable-debug --disable-shared
    make



#### To build on Win32

Choose (Re)Build All from the project workspace

Run the testsuite program





# CyaSSL version 0.9.9 (7/25/2008) 

This release of CyaSSL adds bug fixes, Pre-Shared Keys, over-rideable memory
handling, and optionally TomsFastMath.  Thanks to Moisés Guimarães for the
work on TomsFastMath.

To optionally use TomsFastMath pass --enable-fastmath to ./configure
Or define USE_FAST_MATH in each project from CyaSSL for MSVC.

Please use the benchmark routine before and after to see the performance
difference, on some platforms the gains will be little but RSA encryption
always seems to be faster.  On x86-64 machines with GCC the normal math library
may outperform the fast one when using CFLAGS=-m64 because TomsFastMath can't
yet use -m64 because of GCCs inability to do 128bit division.

     *** UPDATE GCC 4.2.1 can now do 128bit division ***

See notes below (0.2.0) for complete build instructions.


# CyaSSL version 0.9.8 (5/7/2008) 

This release of CyaSSL adds bug fixes, client side Diffie-Hellman, and better
socket handling.

See notes below (0.2.0) for complete build instructions.


# CyaSSL version 0.9.6 (1/31/2008) 

This release of CyaSSL adds bug fixes, increased session management, and a fix
for gnutls.

See notes below (0.2.0) for complete build instructions.


# CyaSSL version 0.9.0 (10/15/2007) 

This release of CyaSSL adds bug fixes, MSVC 2005 support, GCC 4.2 support, 
IPV6 support and test, and new test certificates.

See notes below (0.2.0) for complete build instructions.


# CyaSSL version 0.8.0 (1/10/2007) 

This release of CyaSSL adds increased socket support, for non-blocking writes,
connects, and interrupted system calls.

See notes below (0.2.0) for complete build instructions.


# CyaSSL version 0.6.3 (10/30/2006) 

This release of CyaSSL adds debug logging to stderr to aid in the debugging of
CyaSSL on systems that may not provide the best support.

If CyaSSL is built with debugging support then you need to call
CyaSSL_Debugging_ON() to turn logging on.

On Unix use ./configure --enable-debug

On Windows define DEBUG_CYASSL when building CyaSSL


To turn logging back off call CyaSSL_Debugging_OFF()

See notes below (0.2.0) for complete build instructions.


# CyaSSL version 0.6.2 (10/29/2006) 

This release of CyaSSL adds TLS 1.1.

Note that CyaSSL has certificate verification on by default, unlike OpenSSL.
To emulate OpenSSL behavior, you must call SSL_CTX_set_verify() with
SSL_VERIFY_NONE.  In order to have full security you should never do this, 
provide CyaSSL with the proper certificates to eliminate impostors and call
CyaSSL_check_domain_name() to prevent man in the middle attacks.

See notes below (0.2.0) for build instructions.

# CyaSSL version 0.6.0 (10/25/2006) 

This release of CyaSSL adds more SSL functions, better autoconf, nonblocking
I/O for accept, connect, and read.  There is now an --enable-small configure
option that turns off TLS, AES, DES3, HMAC, and ERROR_STRINGS, see configure.in
for the defines.  Note that TLS requires HMAC and AES requires TLS.

See notes below (0.2.0) for build instructions.


# CyaSSL version 0.5.5 (09/27/2006) 

This mini release of CyaSSL adds better input processing through buffered input
and big message support.  Added SSL_pending() and some sanity checks on user
settings.

See notes below (0.2.0) for build instructions.


# CyaSSL version 0.5.0 (03/27/2006) 

This release of CyaSSL adds AES support and minor bug fixes. 

See notes below (0.2.0) for build instructions.


# CyaSSL version 0.4.0 (03/15/2006)

This release of CyaSSL adds TLSv1 client/server support and libtool. 

See notes below for build instructions.


# CyaSSL version 0.3.0 (02/26/2006)

This release of CyaSSL adds SSLv3 server support and session resumption. 

See notes below for build instructions.


# CyaSSL version 0.2.0 (02/19/2006)


This is the first release of CyaSSL and its crypt brother, CTaoCrypt.  CyaSSL
is written in ANSI C with the idea of a small code size, footprint, and memory
usage in mind.  CTaoCrypt can be as small as 32K, and the current client
version of CyaSSL can be as small as 12K.


The first release of CTaoCrypt supports MD5, SHA-1, 3DES, ARC4, Big Integer
Support, RSA, ASN parsing, and basic x509 (en/de)coding.

The first release of CyaSSL supports normal client RSA mode SSLv3 connections
with support for SHA-1 and MD5 digests.  Ciphers include 3DES and RC4.


#### To build on Linux, Solaris, *BSD, Mac OS X, or Cygwin:

    ./configure
    make

    from the ./testsuite/ directory run ./testsuite 

#### to make a debug build:

    ./configure --enable-debug --disable-shared
    make



#### To build on Win32

Choose (Re)Build All from the project workspace

Run the testsuite program



*** The next release of CyaSSL will support a server and more OpenSSL
compatibility functions.


Please send questions or comments to todd@wolfssl.com
