# marik build

Madeira v0.1.3 with these changes, built by `.github/workflows/marik-build.yml`
and grafted into the official v0.1.3 IPA:

- PR #248 commit 8fc6a0b: LSE atomics (LDADD/LDCLR/LDEOR/LDSET, CAS) on RWX
  pages are emulated through the RW alias. GOG / Inno Setup installers died on
  an LDSETAL into their own code pages.
- `MADEIRA_GDI_SHARED_SECTION` defaults to 1 in every session (WineProcessBridge.m):
  32-bit programs started from a Desktop session faulted on the GDI handle table.
- `env.MADEIRA_TOUCH_HYBRID = 1`: the touch trackpad is a pointer while the program
  shows its cursor and mouse-look while it hides it (ContentView.swift).
- `overlay/`: prebuilt DLLs copied over the bundle
  - `aarch64-windows/wow64win.dll`: class atoms are not pointers (madeira/wow64win-atom-fix.patch)
  - `i386-windows/d3d9-emulated.dll`: DXMT d3d9 zeroes each packed constant block (Postal 2 purple flicker)
  - `arm64ec-windows/wintypes.dll`: missing Wine module for Unity IL2CPP (issue #230)
