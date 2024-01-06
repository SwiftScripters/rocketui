# Maintainer : S4NDM4N <sadaruwan12 at gmail dot com>

pkgname=rocketui
pkgver=1.0.1
pkgrel=1
pkgdesc="An alternative user interface based on Xfce desktop environment."
arch=('any')
url="https://github.com/SwiftScripters/${pkgname}.git"
license=('GPL')
depends=(
        'appmenu-gtk-module-git'
        'dbus'
        'dconf'
        'ffmpegthumbnailer'
        'linux-firmware'
        'hardinfo'
        'lightdm'
        'lightdm-slick-greeter'
        'papirus-icon-theme'
        'pavucontrol'
        'pipewire-audio'
        'plank'
        'tumbler'
        'tumbler-extra-thumbnailers'
        'thunar'
        'thunar-archive-plugin'
        'thunar-media-tags-plugin'
        'thunar-volman'
        'ulauncher'
        'vala-panel-git'
        'vala-panel-appmenu-xfce-git'
        'vala-panel-appmenu-registrar-git'
        'vala-panel-appmenu-common-git'
        'xfce4-appfinder'
        'xf86-input-libinput'
        'xfce4-appfinder'
        'xfce4-battery-plugin'
        'xfce4-datetime-plugin'
        'xfce4-mount-plugin'
        'xfce4-netload-plugin'
        'xfce4-notifyd'
        'xfce4-panel'
        'xfce4-power-manager'
        'xfce4-pulseaudio-plugin'
        'xfce4-screensaver'
        'xfce4-screenshooter'
        'xfce4-session'
        'xfce4-settings'
        'xfce4-taskmanager'
        'xfce4-terminal'
        'xfce4-wavelan-plugin'
        'xfce4-xkb-plugin'
        'xfconf'
        'xfdashboard-git'
        'xfdesktop'
        'xfsprogs'
        'xfwm4'
        'xfwm4-themes'
        'xdg-desktop-portal-gtk'
        'xf86-input-libinput'
        'yaru-gtk-theme'
        'yaru-icon-theme'
        'yaru-sound-theme'
        'yaru-xfwm4-theme'
        )
source=("${pkgname}::git+https://github.com/SwiftScripters/${pkgname}.git")
sha256sums=('SKIP')

package() {
    skelPath=/etc/skel
    usrSharePath=/usr/share
    usrBinPath=/usr/bin
    usrSharePathSource=/usr/share
    usrBinPathSource=/usr/bin

    # Creating folders
    mkdir -p "${pkgdir}${skelPath}/.config"
    mkdir -p "${pkgdir}${skelPath}/.config/autostart"
    mkdir -p "${pkgdir}${skelPath}/.config/plank"
    mkdir -p "${pkgdir}${skelPath}/.config/plank/dock1/launchers"
    mkdir -p "${pkgdir}${skelPath}/.config/rofi"
    mkdir -p "${pkgdir}${skelPath}/.config/rofi/colors"
    mkdir -p "${pkgdir}${skelPath}/.config/rofi/launchers"
    mkdir -p "${pkgdir}${skelPath}/.config/rofi/launchers/type-3"
    mkdir -p "${pkgdir}${skelPath}/.config/rofi/scripts"
    mkdir -p "${pkgdir}${skelPath}/.config/ulauncher"
    mkdir -p "${pkgdir}${skelPath}/.config/ulauncher/user-themes"
    mkdir -p "${pkgdir}${skelPath}/.config/ulauncher/user-themes/RocketLauncher"
    mkdir -p "${pkgdir}${skelPath}/.config/xfce4"
    mkdir -p "${pkgdir}${skelPath}/.config/xfce4/desktop"
    mkdir -p "${pkgdir}${skelPath}/.config/xfce4/panel"
    mkdir -p "${pkgdir}${skelPath}/.config/xfce4/terminal"
    mkdir -p "${pkgdir}${skelPath}/.config/xfce4/xfconf"
    mkdir -p "${pkgdir}${skelPath}/.config/xfce4/xfconf/xfce-perchannel-xml"

    mkdir -p "${pkgdir}${usrSharePath}/doc/${pkgname}"
    mkdir -p "${pkgdir}${usrSharePath}/applications"
    mkdir -p "${pkgdir}${usrSharePath}/icons"
    mkdir -p "${pkgdir}${usrSharePath}/themes"
    mkdir -p "${pkgdir}${usrSharePath}/plank/themes"
    mkdir -p "${pkgdir}${usrSharePath}/plank/themes/rocketplank"

    # Going in to the folder with files.
    # cd "${pkgname}"

    # Installing readme.
    install -Dm644 "README.md" -t "${pkgdir}${usrSharePath}/doc/${pkgname}"

    # Installing license.
    install -Dm644 "LICENSE" -t "${pkgdir}${usrSharePath}/licenses/$pkgname/"

    # Starting the installation.
    for i in autostart cortile plank rofi ulauncher xfce4; do
       cp -r ".config/${i}" "${pkgdir}${skelPath}/.config/"
    done

    cp plankthemesettings/docks.ini "${pkgdir}${skelPath}/.config"
    cp ${usrSharePathSource}/applications/* "${pkgdir}${usrSharePath}/applications"
    cp ${usrSharePathSource}/icons/* "${pkgdir}${usrSharePath}/icons"
    cp -r "${usrBinPathSource}/themes/*" "${pkgdir}${usrSharePath}/themes"
    cp -r ${usrSharePathSource}/plank/themes/rocketplank "${pkgdir}${usrSharePath}/plank/themes"
    install -Dm755 "etc/xdg/xdg-rocket/.bashrc" -t "${pkgdir}/etc/xdg/xdg-rocket"
    install -Dm755 "etc/xdg/xdg-rocket/.xinitrc" -t "${pkgdir}/etc/xdg/xdg-rocket"
    install -Dm755 "etc/xdg/xdg-rocket/xinitrc" -t "${pkgdir}/etc/xdg/xdg-rocket"
    install -Dm644 "etc/lightdm/lightdm.conf.d/60-rocket.conf" -t "${pkgdir}/etc/lightdm/lightdm.conf.d"
    install -Dm644 "${usrSharePathSource}/xessions/Rocket.xsession" -t "${pkgdir}${usrSharePath}/xsessions"

    # Setting the current system to use rocket Ui.
    if ! [[ -d "${homedir}/.config" ]]; then
        mkdir -p "${homedir}/.config"
    fi

    for i in autostart cortile plank rofi ulauncher xfce4; do
        cp -r "${skelPath}/.config/${i}" "${homedir}/.config"
        chown -cR "${USER}:${USER}" "${homedir}/.config/${i}"
    done

    if ! [[ -f "${homedir}/.config/docks.ini" ]]; then
        cp -r "${skelPath}/.config/docks.ini" "${homedir}/.config"
    fi

    chown -cR "${USER}:${USER}" "${homedir}/.config/docks.ini"

    cp "/etc/xdg/xdg-rocket/.bashrc" "${homedir}/.bashrc"
    papirus-folders -C violet --theme Papirus-Dark
}