fuzzel(1)                          General Commands Manual                          fuzzel(1)

NAME
       fuzzel - Wayland app launcher and picker

SYNOPSIS
       fuzzel [OPTIONS]...

DESCRIPTION
       As a launcher, fuzzel lists all available XDG applications in a searchable window.

       With  the --dmenu flag, fuzzel works like a general-purpose picker like dmenu, rofi or
       fzf. Options to choose from are provided on the  STDIN  and  the  selected  option  is
       printed to STDOUT.

       The search box supports Emacs-like key bindings.

       Many things can be configured with fuzzel.ini(5) or command line options:

       --config=PATH
           Path to configuration file, see fuzzel.ini(5) for details.

       --check-config
           Verify configuration and then exit with 0 if ok, otherwise exit with 1.

       --cache=PATH
           Use  a  custom  cache  location.  Fuzzel uses this file to cache the most commonly
           launched applications (to be able to sort them at the top).

           You can also use this option to enable caching of dmenu entries. It is recommended
           that you use a separate cache file for each "type" of dmenu invocation;  i.e.  one
           for the browser history, another for emojis etc.

           Set to /dev/null to disable caching.

           Default: XDG_CACHE_HOME/fuzzel

       -o,--output=OUTPUT
           Specifies  the  monitor  to display the window on. Autocompletion is available for
           zsh and fish, or you can list the available outputs with wlr-randr  or  with  Sway
           using swaymsg -t get_outputs.

           Example: DP-1

           Default: Let the compositor choose output.

       -f,--font=FONT[,FALLBACK1,FALLBACK2,...]
           Comma  separated  list  of primary font, and fallback fonts, in FontConfig format.
           See FONT FORMAT. Default: monospace.

       --use-bold
           Allow fuzzel to use bold fonts.

       -D,--dpi-aware=no|yes|auto
           When set to yes, fonts are sized using the monitor's DPI, making a font of a given
           point size have the same physical size, regardless of monitor.

           In this mode, the monitor's scaling factor is ignored; doubling the scaling factor
           will not double the font size.

           When set to no, the monitor's DPI is ignored. The font is instead sized using  the
           monitor's scaling factor; doubling the scaling factor does double the font size.

           Finally,  if set to auto, fonts will be sized using the monitor's DPI if all moni‐
           tors have a scaling factor of 1. If at least  one  monitor  as  a  scaling  factor
           larger  than  1 (regardless of whether the fuzzel window is mapped on that monitor
           or not), fonts will be scaled using the scaling factor.

           Note that this option typically does not work with bitmap fonts, which  only  con‐
           tains a pre-defined set of sizes, and cannot be dynamically scaled. Whichever size
           (of the available ones) that best matches the DPI or scaling factor, will be used.

           Also  note  that  if the font size has been specified in pixels (:pixelsize=N, in‐
           stead of :size=N), DPI scaling (dpi-aware=yes) will have no effect (the  specified
           pixel  size  will  be used as is). But, if the monitor's scaling factor is used to
           size the font (dpi-aware=no), the font's pixel size will be  multiplied  with  the
           scaling factor.

           Default: auto

       -p,--prompt=PROMPT
           Prompt to use. Default: > .

       --prompt-only=PROMPT
           Same as --prompt, but in --dmenu mode it also:
           •   does not read anything from STDIN
           •   sets --lines to 0

           In non-dmenu mode it behaves exactly like --prompt.

       --placeholder=TEXT
           Text to display as placeholder in the input box. Default: empty.

       --search=TEXT
           Initial  search/filter string. This option pre-fills the input box with the speci‐
           fied string, letting you pre-filter the result.

       -i
           Ignored; for compatibility with other, similar utilities (where -i means "case in‐
           sensitive search").

       --icon-theme=NAME
           Icon theme to use. Note that this option is case sensitive; the  name  must  match
           the theme's folder name.

           Example: Adwaita.

           Default: hicolor.

       -I,--no-icons
           Do not render any icons.

       -F,--fields=FIELDS
           Comma separated list of XDG Desktop entry fields to match against:

           •   filename: the .desktop file's filename
           •   name: the application's name (title)
           •   generic: the application's generic name
           •   exec:  the  applications's executable, as specified in the desktop file. Note:
               may include command line options as well.
           •   keywords: the application's keywords
           •   categories: the application's categories
           •   comment: the application's comment

           Default: filename,name,generic

       --password=[CHARACTER]
           Password input. Render all typed text as CHARACTER. If CHARACTER is omitted,  a  *
           will be used.

       -T,--terminal=TERMINAL ARGS
           Command  to launch XDG applications with the property Terminal=true (htop, for ex‐
           ample). Example: xterm -e. Default: not set.

       -a,--anchor=ANCHOR
           Set window anchor, i.e. where on screen the window will  be  displayed.   You  can
           choose one from:

           •   top-left
           •   top
           •   top-right
           •   left
           •   center
           •   right
           •   bottom-left
           •   bottom
           •   bottom-right

           Default: center

       --x-margin=MARGIN
           Horizontal margin away from the anchor point in pixels. Default: 0.

           Note: this option has no effect when anchor=center, top or bottom.

       --y-margin=MARGIN
           Vertical margin away from the anchor point in pixels. Default: 0.

           Note: this option has no effect when anchor=center, left or right.

       --select=STRING
           Select the first entry that matches the given string (case insensitive).

       -l,--lines=COUNT
           The  (maximum)  number of matches to display. This dictates the window height. De‐
           fault: 15.

       -w,--width
           Window width, in characters. Margins and borders not included. Default: 30.

       --tabs=COUNT
           Number of spaces a tab is expanded to. Default: 8.

       -x,--horizontal-pad=PAD
           Horizontal padding between border and icons and text. In pixels, subject to output
           scaling. Default: 40.

       -y,--vertical-pad=PAD
           Vertical padding between border and text. In pixels, subject  to  output  scaling.
           Default: 8.

       -P,--inner-pad=PAD
           Vertical padding between prompt and match list. In pixels, subject to output scal‐
           ing. Default: 0.

       -b,--background=HEX
           Background color. See COLORS. Default: fdf6e3ff.

       -t,--text-color=HEX
           Text color. See COLORS. Default: 657b83ff.

       --prompt-color=HEX
           Text (foreground) color of prompt character(s). See COLORS. Default: 586e75ff.

       --placeholder-color=HEX
           Text (foreground) color of the placeholder string. See COLORS. Default: 93a1a1ff.

       --input-color=HEX
           Text (foreground) color of input string. See COLORS. Default: 657b83ff.

       -m,--match-color=HEX
           The  color  of  matching  substring(s). As you start typing in the search box, the
           matching part in each application's name is highlighted with this color. See  COL‐
           ORS. Default: cb4b16ff.

       -s,--selection-color=HEX
           The  color to use as background of the currently selected application. See COLORS.
           Default: eee8d5ff.

       -S,--selection-text-color=HEX
           The text color  of  the  currently  selected  application.  See  COLORS.  Default:
           586e75ff.

       -M,--selection-match-color=HEX
           The  color  of matching substring(s) of the currently selected application. As you
           start typing in the search box, the matching part in each  application's  name  is
           highlighted with this color. See COLORS. Default: cb4b16ff.

       --counter-color=HEX
           The  color  of  the  match count stats printed at the right-hand side of the input
           prompt. See COLORS. Default: 93a1a1ff.

       -B,--border-width=INT
           The width of the surrounding border, in pixels (subject to  output  scaling).  De‐
           fault: 1.

       -r,--border-radius=INT
           The  corner  curvature,  subject to output scaling. Larger means more rounded cor‐
           ners. 0 disables rounded corners. Default: 10.

       -C,--border-color=HEX
           The color of the border. See COLORS. Default: 002b36ff.

       --show-actions
           Include desktop actions in the list. Desktop actions are alternative actions  some
           desktop entries have. Examples include "New Window", "New Document", etc.

       --match-mode=exact|fzf|fuzzy
           Defines  how  what you type is matched. See fuzzel.ini(5) for details. The default
           is fzf.

       --no-sort
           Do not sort the result.

       --counter
           Display the match count.

       --filter-desktop=[no]
           Filter the visible desktop entries based on the value of  XDG_CURRENT_DESKTOP.  If
           the optional parameter is "no", explicitly disables filtering.

       --fuzzy-min-length=VALUE
           Search strings shorter than this will not by fuzzy matched. Default: 3.

       --fuzzy-max-length-discrepancy=VALUE
           Maximum  allowed  length  difference between the search string, and a fuzzy match.
           Larger values result in more fuzzy matches. Default: 2.

       --fuzzy-max-distance=VALUE
           Maximum allowed levenshtein distance between the search string, and a fuzzy match.
           Larger values result in more fuzzy matches. Default: 1.

       --line-height=HEIGHT
           Override line height from font metrics. In points by default, but can be specified
           as pixels by appending 'px' (i.e. --line-height=16px). Default: not set.

       --letter-spacing=AMOUNT
           Additional space between letters. In points by default, but can  be  specified  as
           pixels by appending 'px' (i.e. letter-spacing=5px). Negative values are supported.
           Default: 0.

       --layer=top|overlay
           Which layer to render the fuzzel window on. Valid values are top and overlay.

           top  renders above normal windows, but typically below fullscreen windows and lock
           screens.

           overlay renders on top of both normal windows and fullscreen  windows.  Note  that
           the  order  is  undefined  if  several windows use the same layer. Since e.g. lock
           screens typically use overlay, that means fuzzel may or may not appear on top of a
           lock screen.

           Default: top

       --no-exit-on-keyboard-focus-loss
           Do not exit when losing keyboard focus. This can be useful  on  compositors  where
           enabling "focus-follows-mouse" causes fuzzel to exit as soon as the mouse is moved
           over another window. Sway (at least up to, and including 1.7) exhibits this behav‐
           ior.

       --launch-prefix=COMMAND
           Command to launch XDG applications with. If set, fuzzel will pass the Desktop File
           ID  of  the  chosen  application  (see  the  Desktop  Entry  specification) in the
           FUZZEL_DESKTOP_FILE_ID environment variables. Default: not set.

       --list-executables-in-path
           Include executables from the PATH environment variable. Applies to the normal  ap‐
           plication mode, not the dmenu mode.

       --render-workers=COUNT
           Number  of  threads  to use for rendering. Set to 0 to disable multithreading. De‐
           fault: the number of available logical CPUs (including SMT). Note that this is not
           always the best value. In some cases, the number of physical cores is better.

       --match-workers=COUNT
           Number of threads to use for matching. Set to 0  to  disable  multithreading.  De‐
           fault: the number of available logical CPUs (including SMT). Note that this is not
           always the best value. In some cases, the number of physical cores is better.

       --delayed-filter-ms=TIME_MS
           Time, in milliseconds, to delay refiltering when there are more matches than --de‐
           layed-filter-limit. Default: 300.

       --delayed-filter-limit=N
           When  there  are  more matches than this, switch from immediate refiltering to de‐
           layed refiltering (see --delayed-filter-ms). Default: 20000.

       -d,--dmenu
           dmenu compatibility mode. In this mode, the list entries are read from stdin (new‐
           line separated). The selected entry is printed to stdout. If the input string does
           not match any of the entries, the input string is printed as is on stdout.

           Alternatively, you can symlink the fuzzel binary to dmenu. Fuzzel will then  start
           in dmenu mode, without the --dmenu argument.

           Fuzzel  also  supports icons, using Rofi's extended dmenu protocol. To set an icon
           for an entry, append \0icon\x1f<icon-name>. Example:

               echo -en "Firefox\0icon\x1ffirefox" | fuzzel --dmenu

       --dmenu0
           Like --dmenu, but input is NUL separated instead of newline separated.  Note  that
           in this mode, icons are not supported.

       --index
           Print selected entry's index instead of its text. Index values start with zero for
           the first entry. dmenu mode only.

       -R,--no-run-if-empty
           Exit immediately, without showing the UI, if stdin is empty. dmenu mode only.

       --log-level={info,warning,error,none}
           Log level, used both for log output on stderr as well as syslog. Default: warning.

       --log-colorize=[{never,always,auto}]
           Enables or disables colorization of log output on stderr.

       --log-no-syslog
           Disables syslog logging. Logging is only done on stderr.

       -v,--version
           Show the version number and quit

CONFIGURATION
       fuzzel will search for a configuration file in the following locations, in this order:

           •   XDG_CONFIG_HOME/fuzzel/fuzzel.ini  (defaulting  to ~/.config/fuzzel/fuzzel.ini
               if unset)
           •   XDG_CONFIG_DIRS/fuzzel/fuzzel.ini (defaulting to /etc/xdg/fuzzel/fuzzel.ini if
               unset)

       An example configuration file containing all options with  their  default  value  com‐
       mented out will usually be installed to /etc/xdg/fuzzel/fuzzel.ini.

       For more information, see fuzzel.ini(5).

LOCALIZATION
       Fuzzel uses the localized strings from the .desktop files by default. To disable this,
       run fuzzel with LC_MESSAGES=C.

FONT FORMAT
       The  font  is  specified in FontConfig syntax. That is, a colon-separated list of font
       name and font options.

       Examples:
       •   Dina:weight=bold:slant=italic
       •   Arial:size=12

COLORS
       All colors must be specified as a RGBA quadruple, in hex  format,  without  a  leading
       '0x'.

       EXAMPLES:
       •   white: ffffffff (no transparency)
       •   black: 000000ff (no transparency)
       •   black: 00000010 (semi-transparent)
       •   red: ff0000ff (no transparency)

       The default color scheme is Solarized.

FILES
       $XDG_CACHE_HOME/fuzzel
           Stores  a  list of applications and their launch count. This allows fuzzel to sort
           frequently launched applications at the top.

       $XDG_RUNTIME_DIR/fuzzel-$WAYLAND_DISPLAY.lock
           Lock file, used to prevent multiple fuzzel instances  from  running  at  the  same
           time.

SEE ALSO
       •   fuzzel.ini(5)
       •   https://specifications.freedesktop.org/desktop-entry-spec/desktop-entry-spec-lat‐
           est.html
       •   https://codeberg.org/dnkl/fuzzel

                                          2024-09-09                                fuzzel(1)
