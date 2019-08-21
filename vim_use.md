# All About Vim

<!-- TOC -->

- [Vim Encoding](#vim-encoding)
    - [Set encoding and fileencoding to utf-8 in Vim](#set-encoding-and-fileencoding-to-utf-8-in-vim)
    - [Set file BOM](#set-file-bom)
- [Other Character Encoding Tricks for Vim](#other-character-encoding-tricks-for-vim)
    - [open a file for editing  using the specified encoding](#open-a-file-for-editing--using-the-specified-encoding)
    - [save a file in a specified encoding](#save-a-file-in-a-specified-encoding)
    - [specifies the character encoding used internally](#specifies-the-character-encoding-used-internally)
    - [specifies the character encoding used for saving files](#specifies-the-character-encoding-used-for-saving-files)
    - [displays the code point of the character under the cursor](#displays-the-code-point-of-the-character-under-the-cursor)
    - [displays the hexadecimal value of the bytes under the cursor](#displays-the-hexadecimal-value-of-the-bytes-under-the-cursor)
    - [identifies any invalid UTF-8 character sequences](#identifies-any-invalid-utf-8-character-sequences)

<!-- /TOC -->


## Vim Encoding

### Set encoding and fileencoding to utf-8 in Vim

REF: [vimdoc options](http://vimdoc.sourceforge.net/htmldoc/options.html#%27bomb%27/)

- In the first case with 

        :set encoding=utf-8

    you'll change the output encoding that is shown in the terminal.

- In the second case with 

        :set fileencoding=utf-8
        
    you'll change the output encoding of the file that is written.

- you can set them both in your `~/.vimrc` if you always want to work in utf-8

### Set file BOM

- Also note that UTF8 files often begin with a Byte Order Mark (BOM) which indicates endianness. The BOM is optional but some programs use it exclusively to determine the file encoding. Under certain conditions Vim will write the BOM but sometimes it won't. To explicitly set the BOM do this:

        :set bomb

## Other Character Encoding Tricks for Vim

REF: [character-encoding-tricks-for-vim](https://spin.atomicobject.com/2011/06/21/character-encoding-tricks-for-vim/)

### open a file for editing  using the specified encoding

    :edit ++enc=<encoding> [filename]

This command allow you to open (or re-open) a file for editing in Vim using the specified encoding. This can be very useful if, for example, you are editing a file encoded in UTF-8, but Vim has auto-detected it as Latin-1.

### save a file in a specified encoding

    :write ++enc=<encoding> [filename]

### specifies the character encoding used internally

    :set encoding[=<encoding>]

If no encoding is specified, the current encoding will be displayed.

### specifies the character encoding used for saving files

    :set fileencoding[=<encoding>]

### displays the code point of the character under the cursor

    :as or keystroke: ga

You may also use the much easier keyboard shortcut `ga`. The decimal, hexadecimal, and octal code point values will be displayed. For example, the Greek Letter Omega, in UTF-8, provides: “<Ω> 937, Hex 03a9, Octal 1651”. ’03a9′ is the hexadecimal code point value, in Unicode, for Omega.

### displays the hexadecimal value of the bytes under the cursor

    keystroke: g8


### identifies any invalid UTF-8 character sequences

    keystroke: 8g8

For example, if the file is encoded as UTF-8, but contains a byte or set of bytes which do not represent a valid UTF-8 character, this command will position the cursor over that location in the file. Generally, Vim will represent this invalid character sequence as the hexadecimal value of the byte or bytes enclosed in angle brackets, such as “<93>”.

Searching through the Vim manual reveals several more features which can also be handy, such as the ability to edit text files by hexadecimal value using the xxd utility, support for the Unicode byte-order mark (BOM), and modifying how the keyboard encodes what is typed.