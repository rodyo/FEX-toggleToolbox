[![View toggleToolbox on File Exchange](https://www.mathworks.com/matlabcentral/images/matlab-file-exchange.svg)](https://www.mathworks.com/matlabcentral/fileexchange/60347-toggletoolbox) 

[![Donate to Rody](https://i.stack.imgur.com/bneea.png)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=4M7RMVNMKAXXQ&source=url)

Toggle MATLAB toolbox on or off. This allows you to test whether your multi-developer codebase indeed has the exact toolbox dependencies you think it has. 

`S = TOGGLETOOLBOX()`, `S = TOGGLETOOLBOX('')` or `S = TOGGLETOOLBOX('all')` queries the on/off states of all installed
toolboxes.

`M = TOGGLETOOLBOX('names')` returns the full names / directory names map `[M]` applicable to the current MATLAB installation.

`S = TOGGLETOOLBOX(toolbox, state)` queries or sets the on/off state of the MATLAB toolbox `[toolbox]` to `[state]`. The string or cellstring `[toolbox]` may be equal to the toolbox' installation directory name (the same as used by `ver()`), or the toolbox' full name. The string `[state]` may be one of `'on'`, `'off'` or `'query'`. The return argument `[S]` is a structure containing the
toolbox name(s) as fields, with the on/off state represented as `true`/`false`.

`S = TOGGLETOOLBOX(..., permanency)` for string `[permanency]` equal to `'permanent'` will attempt to make the change persist between different MATLAB sessions. For `[permanency]` equal to `'temporary'` (the default), the change will only last for the remainder of the current session.

`TOGGLETOOLBOX(S0)` will reset the on/off states of all toolboxes to the states contained in `[S0]`, where `[S0]` is a structure previously returned by `TOGGLETOOLBOX()` as outlined above.

Disabling a toolbox is done by removing the relevant directories from the MATLAB path. Since the order of the path is important for name resolution, `TOGGLETOOLBOX()` attempts to keep the order of all paths as close to MATLAB's startup path as possible. Calling `TOGGLETOOLBOX()` multiple times for different toolboxes and arbitrary on/off states should not affect the overall path order -- calling `TOGGLETOOLBOX('all', 'on')` afterwards results in a path identical to the startup path.

Note that `TOGGLETOOLBOX()` generates a `MAT` file for both performance and persistence between MATLAB sessions and across platforms. Please make sure that `TOGGLETOOLBOX()` is located in a directory where it has write access.

EXAMPLE SESSION:

```
>> M = toggleToolbox('names')%
M =
'aero' 'Aerospace Toolbox'
'aeroblks' 'Aerospace Blockset'
'bioinfo' 'Bioinformatics Toolbox'
'comm' 'Communications Toolbox'
...

>> S = toggleToolbox({'Aerospace Toolbox' 'Wavelet Toolbox'}, 'query')
S =
aero: 1
wavelet: 1

>> w = ver('wavelet')
w =
Name: 'Wavelet Toolbox'
Version: '4.5'
Release: '(R2010a)'
Date: '25-Jan-2010'

>> S = toggleToolbox({'Aerospace Toolbox' 'Wavelet Toolbox'}, 'off');
>> toggleToolbox({'Aerospace Toolbox' 'Wavelet Toolbox'}, 'query')
ans =
aero: 0
wavelet: 0

>> w = ver('wavelet')
w =
0x0 struct array with fields:
Name
Version
Release
Date

>> toggleToolbox(S);
>> toggleToolbox({'Aerospace Toolbox' 'Wavelet Toolbox'}, 'query')
ans =
aero: 1
wavelet: 1

>> % Cross-platform developer mode:
>> S = toggleToolbox('all', 'off');
```

If you find this work useful, please [consider a donation](https://www.paypal.com/donate/?token=T_UbreXV6SbNiBBwN8GS3IGWt7B6FTmO14tgJNN0YdKENFBolLR7pJXNAC5NLvMjn9js00&country.x=NZ&locale.x=NZ).

