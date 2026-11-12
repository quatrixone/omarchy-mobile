<!-- SPDX-License-Identifier: MIT -->
# mesa-freedreno-dipper

This package builds Mesa's `msm_dri.so` for Dipper without changing the shared
`mesa` package or installing the driver on other phones. It is built from the
same Mesa source and Omarchy version marker as the shared package, and requires
that exact `mesa` version because the DRI module loads Mesa's `libgallium`.

The package is intended to be listed only in Dipper's `ROOTFS_PACKAGES`. It
contains the DRI driver and its license; all common Mesa libraries come from
the regular shared `mesa` package. `tools/build-packages` treats it as a slow,
named package so routine builds do not compile it for every phone.

The package build checks that the output contains `msm_dri.so` and that it
links to the pinned `libgallium` soname. This does not replace a Dipper
hardware test under Hyprland (`eglinfo` or `glxinfo -B` and `tools/phone-smoke`).
An exact Mesa dependency means this package must be rebuilt when the shared
Mesa package version changes.
