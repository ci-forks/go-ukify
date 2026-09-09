QA proof media for kairos-io/go-ukify#64.

A UKI whose SecureBoot signature and PCR policy signature were both produced
by an RSA key held in SoftHSM, through the `pkcs11:` code path this PR changes.
Booted in QEMU with OVMF Secure Boot enabled, only that HSM certificate in db,
and a swtpm vTPM attached.

- 01-secureboot-uki-splash.png       sd-boot handed off to the HSM-signed UKI
- 02-kernel-boot.png                 kernel running, Secure Boot enabled
- 03-tpm-pcr-barrier.png             systemd-pcrphase-initrd (TPM PCR Barrier) running,
                                     so ConditionSecurity=measured-uki was satisfied
- 04-negative-control-access-denied.png  same ESP with the HSM cert NOT enrolled:
                                     firmware refuses with "Access Denied"
- boot-secureboot-tpm.mp4            the full recorded boot
