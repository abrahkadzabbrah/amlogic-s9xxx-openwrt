# OpenWrt for Amlogic s9xxx tv box

View Chinese description  |  [查看中文说明](README.cn.md)

Support `github.com One-stop compilation`, `Use GitHub Action to packaging`, `Use github.com Releases rootfs file to packaging`, `Local packaging`. including OpenWrt firmware install to EMMC and update related functions. Support Amlogic s9xxx tv box are ***`s922x, s905x3, s905x2, s912, s905d, s905x, s905w, s905`***, etc. such as ***`Belink GT-King, Belink GT-King Pro, UGOOS AM6 Plus, X96-Max+, HK1-Box, H96-Max-X3, Phicomm-N1, Octopus-Planet, Fiberhome HG680P, ZTE B860H`***, etc.

The latest version of the OpenWrt firmware can be downloaded in [Releases](https://github.com/ophub/amlogic-s9xxx-openwrt/releases).

This OpenWrt firmware is packaged using `Flippy's` Amlogic S9xxx Kernel for OpenWrt, and the Install and update scripts, etc. Welcome to use `Fork` for [personalized OpenWrt firmware configuration](https://github.com/ophub/amlogic-s9xxx-openwrt/blob/main/router-config/README.md). If you like it, Please click the `Star`.

## OpenWrt Firmware instructions

| Model  | BOX | [Optional kernel](https://github.com/ophub/kernel/tree/main/pub/stable) | OpenWrt Firmware |
| ---- | ---- | ---- | ---- |
| s922x | [Beelink-GT-King](https://tokopedia.link/RAgZmOM41db), [Beelink-GT-King-Pro](https://www.gearbest.com/tv-box/pp_3008857542462482.html), [Ugoos-AM6-Plus](https://tokopedia.link/pHGKXuV41db), [ODROID-N2](https://www.tokopedia.com/search?st=product&q=ODROID-N2) | All | openwrt_s922x_k*.img |
| s905x3 | [X96-Max+](https://tokopedia.link/uMaH09s41db), [HK1-Box](https://tokopedia.link/xhWeQgTuwfb), [H96-Max-X3](https://tokopedia.link/KuWvwoYuwfb), [Ugoos-X3](https://tokopedia.link/duoIXZpdGgb), [X96-Air](https://www.gearbest.com/tv-box/pp_3002885621272175.html), [A95XF3-Air](https://tokopedia.link/ByBL45jdGgb) | All | openwrt_s905x3_k*.img |
| s905x2 | [X96Max-4G](https://tokopedia.link/HcfLaRzjqeb), [X96Max-2G](https://tokopedia.link/HcfLaRzjqeb) | All | openwrt_s905x2_k*.img |
| s912 | [H96-Pro-Plus](https://tokopedia.link/jb42fsBdGgb), Octopus-Planet | All | openwrt_s912_k*.img |
| s905 | [Beelink-Mini-MX-2G](https://www.gearbest.com/tv-box-mini-pc/pp_321409.html), [MXQ-PRO+4K](https://www.gearbest.com/tv-box-mini-pc/pp_354313.html) | All | openwrt_s905_k*.img |
| s905d | Phicomm-N1 | All | openwrt_s905d_k*.img |
| s905x | [HG680P](https://tokopedia.link/HbrIbqQcGgb), [B860H](https://www.zte.com.cn/global/products/cocloud/201707261551/IP-STB/ZXV10-B860H) | 5.4.* | openwrt_s905x_k*.img |
| s905w | [X96-Mini](https://tokopedia.link/ro207Hsjqeb), [TX3-Mini](https://www.gearbest.com/tv-box/pp_009748238474.html) | 5.4.* | openwrt_s905w_k*.img |

💡Tip: The current box of ***`s905`*** can only be used in `TF/SD/USB`, and other types of boxes can also be used in `EMMC` at the same time.

## Install to EMMC and update instructions

Choose the corresponding firmware according to your box. Then write the IMG file to the USB hard disk through software such as [Rufus](https://rufus.ie/) or [balenaEtcher](https://www.balena.io/etcher/). Insert the USB hard disk into the box. Common for all `Amlogic s9xxx tv box`.

- ### Install OpenWrt

Log in to the default IP: 192.168.1.1 → `Login in to openwrt` → `system menu` → `Amlogic Service` → `Install OpenWrt`

- ### Update OpenWrt

Log in to the default IP: 192.168.1.1 →  `Login in to openwrt` → `system menu` → `Amlogic Service` → `Update OpenWrt`

Tip: Functions such as install/update are provided by [luci-app-amlogic](https://github.com/ophub/luci-app-amlogic) to provide visual operation support. Also supports [command operations](https://github.com/ophub/amlogic-s9xxx-openwrt/blob/main/router-config/README.md#8-install-the-firmware).

- ### Use OpenWrt in TF/USB

Log in to the default IP: 192.168.1.1 →  `Login in to openwrt` → `system menu` → `TTYD terminal` → input command

```yaml
openwrt-tf
```

After activating the remaining space, the kernel and OpenWrt system can be upgraded in TF/USB.

- ### Create swap for openwrt system

If you feel that the memory of the current box is not enough when you are using applications with a large memory footprint such as `docker`, you can create a `swap` virtual memory partition, Change the disk space of `/mnt/*4` A certain capacity is virtualized into memory for use. The unit of the input parameter of the following command is `GB`, and the default is `1`.

Log in to the default IP: 192.168.1.1 →  `Login in to openwrt` → `system menu` → `TTYD terminal` → input command

```yaml
openwrt-swap 1
```

- ### Backup/restore the original EMMC system

Supports backup/restore of the box's `EMMC` partition in `TF/SD/USB`. It is recommended that you back up the Android TV system that comes with the current box before installing the OpenWrt system in a brand new box, so that you can use it in the future when restoring the TV system.

Please start the OpenWrt system from `TF/SD/USB`, Log in to the default IP: 192.168.1.1 →  `Login in to openwrt` → `system menu` → `TTYD terminal` → input command

```yaml
openwrt-ddbr
```

According to the prompt, enter `b` to perform system backup, and enter `r` to perform system recovery.

💡Tip: You must use the `/mnt/*4/` space to store the `BACKUP-arm-64-emmc.img.gz` backup file, Users who have not created the `TF/SD/USB` extended partition must first use the `openwrt-tf` command to create the extended partition.

## Detailed make compile command

| Parameter | Meaning | Description |
| ---- | ---- | ---- |
| -d | Defaults | Compile all cores and all firmware types. |
| -b | Build | Specify the Build firmware type. Write the build firmware name individually, such as `-b s905x3` . Multiple firmware use `_` connect such as `-b s905x3_s905d` . You can use these codes: `s905x3`, `s905x2`, `s905x`, `s905w`, `s905d`, `s905`, `s922x`, `s922x-n2`, `s912`. Note: `s922x-n2` is `s922x-odroid-n2`. |
| -v | Version | Specify the name of the kernel [version branch](https://github.com/ophub/kernel/tree/main/pub), Such as `-v stable`. The specified name must be the same as the branch directory name. The `stable` branch version is used by default. |
| -k | Kernel | Specify the [kernel](https://github.com/ophub/kernel/tree/main/pub/stable) name. Write the kernel name individually such as `-k 5.4.160` . Multiple kernel use `_` connection such as `-k 5.10.80_5.4.160` |
| -a | AutoKernel | Set whether to automatically adopt the latest version of the kernel of the same series. When it is `true`, it will automatically find in the kernel library whether there is an updated version of the kernel specified in `-k` such as 5.4.160 version. If there is the latest version of 5.4 same series, it will automatically Replace with the latest version. When set to `false`, the specified version of the kernel will be compiled. Default value: `true` |
| -s | Size | Specify the size of the root partition in MB. The default is 1024, and the specified size must be greater than 256. Such as `-s 1024` |
| -h | help | View full documentation. |

- `sudo ./make -d -b s905x3 -k 5.4.160`: recommend. Use the default configuration, specify a kernel and a firmware for compilation.
- `sudo ./make -d -b s905x3_s905d -k 5.10.80_5.4.160`: Use the default configuration, specify multiple cores, and multiple firmware for compilation. use `_` to connect.
- `sudo ./make -d`: Compile latest kernel versions of openwrt for all SoC with the default configuration.
- `sudo ./make -d -b s905x3 -k 5.4.160 -s 1024`: Use the default configuration, specify a kernel, a firmware, and set the partition size for compilation.
- `sudo ./make -d -b s905x3 -v stable -k 5.7.19`: Use the default configuration, specify the model, specify the [version branch](https://github.com/ophub/kernel/tree/main/pub), and specify the kernel for packaging.
- `sudo ./make -d -b s905x3_s905d`: Use the default configuration, specify multiple firmware, use `_` to connect. compile all kernels.
- `sudo ./make -d -k 5.10.80_5.4.160`: Use the default configuration. Specify multiple cores, use `_` to connect.
- `sudo ./make -d -k 5.10.80_5.4.160 -a true`: Use the default configuration. Specify multiple cores, use `_` to connect. Auto update to the latest kernel of the same series.
- `sudo ./make -d -k latest`: Use the default configuration to compile the latest kernel version of the openwrt firmware.
- `sudo ./make -d -s 1024 -k 5.4.160`: Use the default configuration and set the partition size to 1024m, and only compile the openwrt firmware with the kernel version 5.4.160.
- `sudo ./make -h`: Display help information and view detailed description of each parameter.
- `sudo ./make`: If you are familiar with the relevant setting requirements of the s905x3 firmware, you can follow the prompts, such as selecting the firmware you want to make, the kernel version, setting the ROOTFS partition size, etc. If you don’t know these settings, just press Enter.

## Compilation and packaging method

Provide multiple ways to generate the OpenWrt firmware you need. Please choose one method you like. Each method can be used independently.

- ### Local packaging instructions

1. Install the necessary packages (E.g Ubuntu 20.04 LTS user)
```yaml
sudo apt-get update -y
sudo apt-get full-upgrade -y
sudo apt-get install -y $(curl -fsSL git.io/ubuntu-2004-openwrt)
```
2. Clone the repository to the local. `git clone --depth 1 https://github.com/ophub/amlogic-s9xxx-openwrt.git`
3. Create a `openwrt-armvirt` folder, and upload the OpenWrt firmware of the ARM kernel ( Eg: `openwrt-armvirt-64-default-rootfs.tar.gz` ) to this `~/amlogic-s9xxx-openwrt/openwrt-armvirt` directory.
4. Name the kernel package according to the corresponding version number, such as `5.4.160` version, and put it into the `~/amlogic-s9xxx-openwrt/amlogic-s9xxx/amlogic-kernel` directory.
5. Enter the `~/amlogic-s9xxx-openwrt` root directory. And run Eg: `sudo ./make` to make selection settings. The generated OpenWrt firmware is in the `out` directory under the root directory.

- ### Github.com One-stop compilation instructions

You can modify the configuration file in the `router-config` directory and `.yml` file, customize the OpenWrt firmware, and complete the packaging online through `Actions`, and complete all the compilation of OpenWrt firmware in github.com One-stop.

1. Personalized plug-in configuration in [router-config](https://github.com/ophub/amlogic-s9xxx-openwrt/tree/main/router-config) directory. Workflows configuration in [.yml](https://github.com/ophub/amlogic-s9xxx-openwrt/blob/main/.github/workflows/build-openwrt-lede.yml) file.
2. Select ***`Build OpenWrt`*** on the [Action](https://github.com/ophub/amlogic-s9xxx-openwrt/actions) page. Click the ***`Run workflow`*** button.

```yaml
- name: Build OpenWrt firmware
  id: build
  run: |
    [ -d openwrt-armvirt ] || mkdir -p openwrt-armvirt
    cp -f openwrt/bin/targets/*/*/*.tar.gz openwrt-armvirt/ && sync
    sudo chmod +x make
    sudo ./make -d -b s905x3_s905x2_s905x_s905w_s905d_s922x_s912 -k 5.10.80_5.4.160
    echo "PACKAGED_OUTPUTPATH=${PWD}/out" >> $GITHUB_ENV
    echo "PACKAGED_OUTPUTDATE=$(date +"%Y.%m.%d.%H%M")" >> $GITHUB_ENV
    echo "::set-output name=status::success"
```

The output variable ${{ env.PACKAGED_OUTPUTPATH }} is the path where the packaged file is located.

- ### Use github.com Releases rootfs file to packaging

If there is an `openwrt-armvirt-64-default-rootfs.tar.gz` file in a [Releases](https://github.com/ophub/amlogic-s9xxx-openwrt/releases) in your repository, you can use this file to directly package the required firmware.

- `openwrt_s9xxx_.*` is Prefix the `tag_name` in the Release.
- `openwrt-armvirt-64-default-rootfs.tar.gz` is the firmware you are going to package, please refer to [router-config](https://github.com/ophub/amlogic-s9xxx-openwrt/tree/main/router-config) for compilation method.

[For more instructions please see: use-releases-file-to-packaging.yml](https://github.com/ophub/amlogic-s9xxx-openwrt/blob/main/.github/workflows/use-releases-file-to-packaging.yml)

```yaml
- name: Build OpenWrt firmware
  id: build
  run: |
    [ -d openwrt-armvirt ] || mkdir -p openwrt-armvirt
    curl -s "https://api.github.com/repos/${GITHUB_REPOSITORY}/releases" | grep -o "openwrt_s9xxx_.*/openwrt-armvirt-.*\.tar.gz" | head -n 1 > DOWNLOAD_URL
    [ -s DOWNLOAD_URL ] && wget -q -P openwrt-armvirt https://github.com/${GITHUB_REPOSITORY}/releases/download/$(cat DOWNLOAD_URL)
    sudo chmod +x make
    sudo ./make -d -b s905x3_s905x2_s905x_s905w_s905d_s922x_s912 -k 5.10.80_5.4.160
    echo "PACKAGED_OUTPUTPATH=${PWD}/out" >> $GITHUB_ENV
    echo "PACKAGED_OUTPUTDATE=$(date +"%Y.%m.%d.%H%M")" >> $GITHUB_ENV
    echo "::set-output name=status::success"
```

This function is suitable for the needs of replacing the [kernel](https://github.com/ophub/kernel/tree/main/pub/stable) packaging and packaging the OpenWrt firmware of the specified [amlogic-dtb](https://github.com/ophub/amlogic-s9xxx-openwrt/tree/main/amlogic-s9xxx/amlogic-dtb) separately. As long as you have the `openwrt-armvirt-64-default-rootfs.tar.gz` file in the [Releases](https://github.com/ophub/amlogic-s9xxx-openwrt/releases) of your repository, you can package the OpenWrt firmware you want at any time, which is efficient and convenient.

- ### Use GitHub Action to packaging instructions

[For more instructions please see: .yml example](https://github.com/ophub/op/blob/main/.github/workflows/build-openwrt-s9xxx.yml)

In your .github/workflows/.yml file, after completing the compilation of Subtarget is ARMv8, add the following online packaging code:

```yaml
- name: Package Armvirt as OpenWrt
  uses: ophub/amlogic-s9xxx-openwrt@main
  with:
    armvirt64_path: openwrt/bin/targets/*/*/*.tar.gz
    amlogic_openwrt: s905x3_s905x2_s905x_s905w_s905d_s922x_s912
    amlogic_kernel: 5.10.80_5.4.160
```

- GitHub Action Input parameter description

| parameter              | Defaults               | Description                                                   |
|------------------------|------------------------|---------------------------------------------------------------|
| armvirt64_path         | no                     | Set the file path of `openwrt-armvirt-64-default-rootfs.tar.gz` , Use the path of the file in the current workflow such as `openwrt/bin/targets/*/*/*.tar.gz` . |
| amlogic_openwrt        | s905d_s905x3           | Set the `SoC` of the packaging box, the default `all` packs all boxes, you can specify a single box such as `s905x3`, you can choose multiple boxes to use `_` connection such as `s905x3_s905d` . SOC code of each box is: `s905x3`, `s905x2`, `s905x`, `s905w`, `s905d`, `s905`, `s922x`, `s922x-n2`, `s912`. Note: `s922x-n2` is `s922x-odroid-n2`. |
| version_branch         | stable                 | Specify the name of the kernel [version branch](https://github.com/ophub/kernel/tree/main/pub), Such as `stable`. The specified name must be the same as the branch directory name. The `stable` branch version is used by default. |
| amlogic_kernel         | 5.10.80_5.4.160        | Set the kernel version，The [kernel](https://github.com/ophub/kernel/tree/main/pub/stable) library contains many original kernels of `Flippy`, you can view and choose to specify. |
| auto_kernel            | true                   | Set whether to automatically adopt the latest version of the kernel of the same series. When it is `true`, it will automatically find in the kernel library whether there is an updated version of the kernel specified in `amlogic_kernel`. such as 5.4.160 version. If there is the latest version of 5.4 same series, it will automatically Replace with the latest version. When set to `false`, the specified version of the kernel will be compiled. Default value: `true` |
| amlogic_size           | 1024                   | Set the size of the firmware ROOT partition |

- GitHub Action Output variable description

| parameter                                | For example             | Description                   |
|------------------------------------------|-------------------------|-------------------------------|
| ${{ env.PACKAGED_OUTPUTPATH }}           | ${PWD}/out              | OpenWrt firmware storage path |
| ${{ env.PACKAGED_OUTPUTDATE }}           | 2021.04.21.1058         | Packing date                  |
| ${{ env.PACKAGED_STATUS }}               | success / failure       | Package status                |

- Uploads OpenWrt Firmware to Release:

```yaml
- name: Upload OpenWrt Firmware to Release
  uses: ncipollo/release-action@v1
  with:
    tag: openwrt_s9xxx
    artifacts: ${{ env.PACKAGED_OUTPUTPATH }}/*
    allowUpdates: true
    token: ${{ secrets.GITHUB_TOKEN }}
    body: |
      This is OpenWrt firmware for Amlogic s9xxx tv box.
      More information ...
```

## Compile a custom kernel

For the compilation method of the custom kernel, see [compile-kernel](https://github.com/ophub/amlogic-s9xxx-armbian/tree/main/compile-kernel)

## ~/openwrt-armvirt/*-rootfs.tar.gz Firmware compilation parameters

| Option | Value |
| ---- | ---- |
| Target System | QEMU ARM Virtual Machine |
| Subtarget | QEMU ARMv8 Virtual Machine(cortex-a53) |
| Target Profile | Default |
| Target Images | tar.gz |

[For more instructions please see: router-config](https://github.com/ophub/amlogic-s9xxx-openwrt/tree/main/router-config)

## Firmware information

| Name | Value |
| ---- | ---- |
| Default IP | 192.168.1.1 |
| Default username | root |
| Default password | password |
| Default WIFI name | OpenWrt |
| Default WIFI password | none |

## Bypass gateway settings

If used as a bypass gateway, you can add custom firewall rules as needed (Network → Firewall → Custom Rules):

```yaml
iptables -t nat -I POSTROUTING -o eth0 -j MASQUERADE        #If the interface is eth0.
iptables -t nat -I POSTROUTING -o br-lan -j MASQUERADE      #If the interface is br-lan bridged.
```

## Acknowledgments

- [OpenWrt](https://github.com/openwrt/openwrt)
- [coolsnowwolf/lede](https://github.com/coolsnowwolf/lede)
- [Lienol/openwrt](https://github.com/Lienol/openwrt)
- [unifreq/openwrt_packit](https://github.com/unifreq/openwrt_packit)

## License

[LICENSE](https://github.com/ophub/op/blob/main/LICENSE) © OPHUB

