<!-- SPDX-License-Identifier: MIT -->
# mesa-freedreno-dipper

This package builds Mesa's Dipper-only Freedreno driver and a separately named
`libgallium` for Dipper without changing the shared `mesa` package or
installing the driver on other phones. Its unique `omamobile5-dipper` marker
keeps this library separate from the shared Mesa library. It requires that
exact `mesa` version so both builds use matching Mesa sources and dependencies.

The package is intended to be listed only in Dipper's `ROOTFS_PACKAGES`. It
contains the DRI driver, the Freedreno Gallium implementation, and its
license; common Mesa libraries come from the regular shared `mesa` package.
`tools/build-packages` treats it as a slow, named package so routine builds do
not compile it for every phone.

The package build checks that the output contains `msm_dri.so` and its matching
`libgallium`. This does not replace a Dipper hardware test under Hyprland
(`eglinfo` or `glxinfo -B` and `tools/phone-smoke`). The package must be rebuilt
when the shared Mesa package version changes.
