# FFmpeg source for ConverAll

[ConverAll](https://play.google.com/store/apps/details?id=com.slaviboy.convertall) converts audio and video on the
device with FFmpeg. It ships FFmpeg as the shared libraries of **FFmpegKit full 8.1.9**
(`dev.ffmpegkit-maintained:ffmpeg-kit-full:8.1.9` on Maven Central), built by the community fork
<https://github.com/ffmpegkit-maintained/ffmpeg> at the tag `v8.1.9-lts-android`.

This repository keeps a copy of the complete source code those libraries were built from, as the GNU Lesser General
Public License asks of anyone who distributes them. ConverAll's own code is not part of it.

## Download

The release [**ffmpeg-kit-full-8.1.9**](https://github.com/slaviboy/convertall-ffmpeg-source/releases/tag/ffmpeg-kit-full-8.1.9)
holds one archive per component: the unmodified source at the tag the build pins (`android-8.1-lts/scripts/source.sh`
in the fork), with [`SHA256SUMS`](SHA256SUMS). The archives are GitHub's own tarballs of those tags.

- `ffmpeg-kit-maintained-v8.1.9-lts-android.tar.gz` is the fork itself: the build script
  (`android-8.1-lts/android.sh`), the scripts and patches it applies, and the source of the FFmpegKit wrapper
  (`libffmpegkit.so` and its Java API).
- `ffmpeg-n8.1.3.tar.gz` is FFmpeg 8.1.3.
- The other archives are the libraries compiled into FFmpeg and the ones they need to build.

## The build

- FFmpeg 8.1.3 configured with `--enable-version3`, and without `--enable-gpl` or `--enable-nonfree`: the libraries are
  covered by the LGPL, version 3 or later. The exact options, read from the shipped `libavutil.so`, are in
  [`CONFIGURE.txt`](CONFIGURE.txt).
- Built with the Android NDK r27c for `arm64-v8a` and `x86_64`.
- In ConverAll's APK they are `lib/arm64-v8a/` and `lib/x86_64/`: `libavcodec.so`, `libavdevice.so`,
  `libavfilter.so`, `libavformat.so`, `libavutil.so`, `libswresample.so`, `libswscale.so`, `libffmpegkit.so` and
  `libffmpegkit_abidetect.so`. ConverAll links them dynamically and does not change them, so they can be replaced
  with a rebuilt copy.
- To rebuild: unpack the fork's archive and run `android-8.1-lts/android.sh --full` with the NDK r27c. The script
  fetches each library at the same tag from the repository listed for it in `scripts/source.sh`; the archives here
  are copies of exactly those tags.

## Components

| Component | Version (tag) | Licence | Archive | SHA-256 |
|---|---|---|---|---|
| FFmpegKit (community fork): build scripts, patches, the FFmpegKit wrapper | `v8.1.9-lts-android` | LGPL-3.0 | `ffmpeg-kit-maintained-v8.1.9-lts-android.tar.gz` (52.9 MB) | `0d18b3514d621a32fe1198303bdceea31bb4862f446602097c00a04bb5d4dc0d` |
| FFmpeg | `n8.1.3` | LGPL-3.0-or-later as configured (`--enable-version3`) | `ffmpeg-n8.1.3.tar.gz` (16.9 MB) | `09f990289327d3ebfedf4fc15cae3f884a65dab7a5aac7bbb5b01ff83900efd9` |
| LAME | `RELEASE__3_100` | LGPL-2.0 (Library GPL) | `lame-RELEASE__3_100.tar.gz` (1.5 MB) | `d390e1754c4e5e702f7ee5a77e849a3c963758cfe5dacc1c64350c68196a29dd` |
| TwoLAME | `0.4.0` | LGPL-2.1 | `twolame-0.4.0.tar.gz` (0.4 MB) | `9f3f03bc9e1038d900f86002c7dce4b49109b3a61544800fc62d71dc51829f05` |
| shine | `3.1.1` | LGPL-2.0 (Library GPL) | `shine-3.1.1.tar.gz` (0.9 MB) | `565b87867d6f8e6616a236445d194e36f4daa9b4e7af823fcf5010af7610c49e` |
| Opus | `v1.4` | BSD-3-Clause | `opus-v1.4.tar.gz` (0.9 MB) | `659e6b223e42a51b0a898632b9a5f406ccd5c2e00aa526ddd1264789774b94e5` |
| libvorbis | `v1.3.7` | BSD-3-Clause | `libvorbis-v1.3.7.tar.gz` (1.2 MB) | `270c76933d0934e42c5ee0a54a36280e2d87af1de3cc3e584806357e237afd13` |
| libtheora | `v1.1.1` | BSD-3-Clause | `libtheora-v1.1.1.tar.gz` (1.1 MB) | `1d5c3b25bbced448f3e741c42df6796e3d5e57136a74bcd68262318290ec2982` |
| Speex | `Speex-1.2.1` | BSD-3-Clause | `speex-Speex-1.2.1.tar.gz` (1.0 MB) | `beaf2642e81a822eaade4d9ebf92e1678f301abfc74a29159c4e721ee70fdce0` |
| opencore-amr | `v0.1.6` | Apache-2.0 | `opencore-amr-v0.1.6.tar.gz` (0.5 MB) | `1f2601c6cd9d47d3ddb2911db832bdc6f5e36c53f5e78937cdc5241ae02cb426` |
| VisualOn AMR-WB encoder | `v0.1.3` | Apache-2.0 | `vo-amrwbenc-v0.1.3.tar.gz` (0.3 MB) | `85c79997ba7ddb9c95b5ddbe9ea032e27595390f3cbd686ed46a69e485cc053c` |
| iLBC | `v3.0.4` | BSD-3-Clause | `libilbc-v3.0.4.tar.gz` (0.2 MB) | `c5ec9e3ec53a0a913f81504e202c7bfefbe9c070b7f5599c5e13a6c75d6af913` |
| SoX Resampler (soxr) | `0.1.3` | LGPL-2.1 | `soxr-0.1.3.tar.gz` (0.1 MB) | `db6ca1b1e8405c6ef92f8294fc123d910abf0a114003b3f0f13fa57a95fd62d0` |
| libvpx | `v1.13.0` | BSD-3-Clause and the WebM patent licence | `libvpx-v1.13.0.tar.gz` (5.5 MB) | `cb2a393c9c1fae7aba76b950bb0ad393ba105409fe1a147ccd61b0aaa1501066` |
| libaom | `v3.6.1` | BSD-2-Clause and the AOM patent licence | `libaom-v3.6.1.tar.gz` (5.3 MB) | `b879e9f6c17106006bf2dff5ffe86d7e7a72dab8f39a51a14e59b86d3abd9e04` |
| dav1d | `1.2.1` | BSD-2-Clause | `dav1d-1.2.1.tar.gz` (1.5 MB) | `2dd85860d213479672b1c708e31593446e8c2b53ff41e2ca25a2eafb718424e2` |
| Kvazaar | `v2.2.0` | BSD-3-Clause | `kvazaar-v2.2.0.tar.gz` (0.6 MB) | `df21f327318d530fe7f2ec65ccabf400690791ebad726d8b785c243506f0e446` |
| OpenH264 | `v2.3.1` | BSD-2-Clause | `openh264-v2.3.1.tar.gz` (60.3 MB) | `453afa66dacb560bc5fd0468aabee90c483741571bca820a39a1c07f0362dc32` |
| libass | `0.17.1` | ISC | `libass-0.17.1.tar.gz` (0.3 MB) | `5ba42655d7e8c5e87bba3ffc8a2b1bc19c29904240126bb0d4b924f39429219f` |
| FreeType | `VER-2-13-0` | FreeType Licence (FTL) | `freetype-VER-2-13-0.tar.gz` (2.5 MB) | `9d71eb9d8e8f250ac70efd4f91168a5327b4804117c4da223e500a11650eed3d` |
| fontconfig | `2.14.2` | MIT-style | `fontconfig-2.14.2.tar.gz` (0.6 MB) | `48d5767819392f42f668075932d26450716930c042f5f970e5b655f807049f86` |
| FriBidi | `v1.0.13` | LGPL-2.1 | `fribidi-v1.0.13.tar.gz` (2.1 MB) | `f24e8e381bcf76533ae56bd776196f3a0369ec28e9c0fdb6edd163277e008314` |
| HarfBuzz | `8.0.1` | "Old MIT" | `harfbuzz-8.0.1.tar.gz` (35.4 MB) | `d54ca67b6a0bf732b66a343566446d7f93df2bb850133f886c0082fb618a06b2` |
| libiconv | `v1.17` | LGPL-2.1 (library) | `libiconv-v1.17.tar.gz` (4.4 MB) | `09d53d6b2b333bfafcce33261feca41d6d0bbc8524ca6606aef171cf2eb56f82` |
| libxml2 | `v2.11.4` | MIT | `libxml2-v2.11.4.tar.gz` (3.8 MB) | `2fd59eccfe277f7b7dec8836254acbebd24af33857a018dd64ddcf92d88d7f7e` |
| Snappy | `1.1.9` | BSD-3-Clause | `snappy-1.1.9.tar.gz` (1.1 MB) | `75c1fbb3d618dd3a0483bff0e26d0a92b495bbe5059c8b4f1c962b478b6e06e7` |
| zimg | `release-3.0.5` | WTFPL | `zimg-release-3.0.5.tar.gz` (0.3 MB) | `a9a0226bf85e0d83c41a8ebe4e3e690e1348682f6a2a7838f1b8cbff1b799bcf` |
| SDL | `release-2.0.8` | zlib | `sdl-release-2.0.8.tar.gz` (5.2 MB) | `9f7541890803ec6ac490af3b49a64d3eb0107e2367aae033fe031d3680a010aa` |
| cpu_features | `v0.8.0` | Apache-2.0 | `cpu-features-v0.8.0.tar.gz` (0.1 MB) | `7021729f2db97aa34f218d12727314f23e8b11eaa2d5a907e8426bcb41d7eaac` |
| expat | `R_2_5_0` | MIT | `expat-R_2_5_0.tar.gz` (8.3 MB) | `ab00ee05c7067fd10a35c5d2a4922ebba746ddd50ff83b79c828da17bbdf1757` |
| libpng | `v1.6.40` | libpng licence | `libpng-v1.6.40.tar.gz` (1.5 MB) | `62d25af25e636454b005c93cae51ddcd5383c40fa14aa3dae8f6576feb5692c2` |
| libuuid | `libuuid-1.0.3` | BSD-3-Clause | `libuuid-libuuid-1.0.3.tar.gz` (0.0 MB) | `39cfe3100eae207d0c8f8f921a3e5a7c12a686833761fcf0ba6805e38312813e` |
| libogg | `v1.3.5` | BSD-3-Clause | `libogg-v1.3.5.tar.gz` (0.3 MB) | `f6f1b04cfa4e98b70ffe775d5e302d9c6b98541f05159af6de2d6617817ed7d6` |
| libsndfile | `1.2.0` | LGPL-2.1 | `libsndfile-1.2.0.tar.gz` (0.7 MB) | `62dc4e2bcd45f6f0e89cbc3522cc90eb174dca0eef0a0d19ead289833b390cd7` |
| gnu-config (config.guess, config.sub; used only to build) | `v20210814` | GPL-3.0 with the Autoconf exception | `config-v20210814.tar.gz` (0.1 MB) | `e7b34eb510ebb76790b2c8e4bfec75393fc5ba121b90f9011a196591f8973228` |

Each archive keeps its own licence files. ConverAll lists the same components, with their licence texts, on its
*Open-source licences* screen.
