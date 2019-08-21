# All About Vim

<!-- TOC -->

- [Vim Encoding](#vim-encoding)
    - [Set encoding and fileencoding to utf-8 in Vim](#set-encoding-and-fileencoding-to-utf-8-in-vim)

<!-- /TOC -->


## Vim Encoding

### Set encoding and fileencoding to utf-8 in Vim

REF: [vimdoc options](http://vimdoc.sourceforge.net/htmldoc/options.html#%27bomb%27/)

1. In the first case with 

        :set encoding=utf-8

    you'll change the output encoding that is shown in the terminal.

1. In the second case with 

        :set fileencoding=utf-8
        
    you'll change the output encoding of the file that is written.

1. you can set them both in your `~/.vimrc` if you always want to work in utf-8

1. Also note that UTF8 files often begin with a Byte Order Mark (BOM) which indicates endianness. The BOM is optional but some programs use it exclusively to determine the file encoding. Under certain conditions Vim will write the BOM but sometimes it won't. To explicitly set the BOM do this:

        :set bomb

