# Impostazioni di CachyOS su T560

1. Durante l'installazione del sistema deselezionare *Firefox*
2. Azzerare tempo di boot

- `sudo nano /etc/default/grub`

- settare ```GRUB_TIMEOUT='0'``` e ```GRUB_TIMEOUT_STYLE=hidden``` a questo punto serve un update di *GRUB* con il comando `sudo grub-mkconfig -o /boot/grub/grub.cfg`  

3. Modificare il file di configurazione della shell *fish* per togliere il lancio di *fastfetch* ad ogni avvio e modifichiamo il tema

- `sudo nano ~/.config/fish/config.fish`

- commentare le tre righe seguenti:
```
function fish_greeting
    riga
end
```  

- Installare uno dei *[Nerd Font](https://github.com/ryanoasis/nerd-fonts?tab=readme-ov-file)*  
- Il mio preferito è *Meslo*:
```
git clone --depth 1 https://github.com/ryanoasis/nerd-fonts.git  
cd nerd-fonts  
./install.sh Meslo  
```
`fc-cache -fv`  

- andiamo nelle Preferenze del terminale e nella sezione del profilo settiamo il nerd font installato come predefinito e *10* come dimensione  

- Installare *[fisher](https://github.com/jorgebucaran/fisher)* + plugin *tide*  
seguiamo i passaggi per configurarlo, le mie scelte:  
**3 (Rainbow) - 1 (True color) - 2 (24-hour format) - 2 (Vertical) - 1 (Sharp) - 1 (Flat) - 4 (Two lines, character and frame) - 3 (Solid) - 2 (Yes) - 4 (Darkest) - 2 (Sparse) - 2 (Many icons) - 2 (Yes) - y (Per sovrascrivere i cambiamenti)**  

- Per terminare possiamo aggiungere qualche configurazione al file `/home/nomeutente/.config/fish/config.fish`  
es. *alias clera clear*  

- Digitare `fish_config` per ulteriori configurazioni  

- Riavviare 

4. Avvio automatico del disco di rete  

- creiamo il punto di mount per i due dischi  

`sudo mkdir -p /mnt/NASm2`  
`sudo nano /etc/fstab`

- aggiungere la seguente riga alla fine del file

```
//192.168.1.192/NASm2 /mnt/NASm2 cifs username=domenico,password=asdcv,rw,uid=1000,gid=1000 0 0
```

5. Installazione della stampante Canon TS3300 e del suo software

`sudo pacman -S cups cups-pdf system-config-printer`
`sudo systemctl enable --now cups`
`sudo pacman -S sane sane-airscan simple-scan`  

6. Per evitare conflitti tra le *WebUi* dei servizi installati nel server andiamo a modificare il file `/etc/hosts` nel seguente modo: 

`sudo nano /etc/hosts`  

- aggiungiamo al file le seguenti linee  

```
192.168.1.xxx   pi.hole  
192.168.1.xxx   webmin.local  
192.168.1.xxx   portainer.local  
```
7. *script* per **mpv** da aggiungere nella cartella */home/.config/mpv/scripts*: **[autoload.lua](https://github.com/mpv-player/mpv/blob/master/TOOLS/lua/autoload.lua)** - **[blacklist-extensions.lua](https://github.com/occivink/mpv-scripts/blob/master/scripts/blacklist-extensions.lua)**

- File da aggiungere nella cartella */home/.config/mpv/script-opts*:  

### autoload.conf  
```
directory_mode=ignore
```

### blacklist_extension.conf
```
# only one of blacklist, whitelist should be defined at a time

# only allow video and image formats
whitelist=mkv,webm,mp4,avi

# alternatively, blacklist formats commonly found near videos
#blacklist=srt,ass,mks,mka,png,jpg,jpeg,gif

remove_files_without_extension=yes

# if the script should be applied only at the beginning, or anytime the playlist changes
oneshot=yes
```

- Per poter scorrere tra i file di una cartella con i tasti *PG ↑ & PG ↓* creare il file *input.conf* nella cartella */home/.config/mpv* con le seguenti righe:

```
PGUP playlist-prev ; show-text "${playlist-pos-1}/${playlist-count}"
PGDWN playlist-next ; show-text "${playlist-pos-1}/${playlist-count}"
```

8. ## Software

- Floorp
- Telegram Desktop
- LibreOffice
- Code OSS  
