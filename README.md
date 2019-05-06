# Xcode Redirect


## Description

Use this file to help Xcode behave more like a command line shell when it
comes to dealing with file redirection. This addresses missing functionality
for:

    * Input redirection (cin >>): < inputfilename
    * Output redirection (cout <<): > outputfilename
    * Error redirection (cerr <<): 2> errorfilename


## How to use it


### Download

First, [download the file directly] or use `curl` or `wget`.

```bash
% wget https://gitlab.umich.edu/eecs281/xcode_redirect/raw/master/xcode_redirect.hpp

or

% curl -O https://gitlab.umich.edu/eecs281/xcode_redirect/raw/master/xcode_redirect.hpp
```


### Add it to your project

In your Project Navigator or through the File Menu, you can "Add Files..." to
your project.

Navigator:
![alt text][add-files navigator]

File Menu:
![alt text][add-files menu]

Navigate to the downloaded copy of `xcode_redirect.hpp` and add it to the
project with the following settings:

Settings:
![alt text][add-files settings]


### Add redirections as needed

In the main editor window or through the Project Menu, you can
"Edit Scheme..." to add command line parameters and file redirections.

Editor:
![alt text][edit-scheme editor]

Project Menu:
![alt text][edit-scheme menu]

For each file redirection, include an entry in "Arguments Passed On Launch."
Be sure to start with a redirection (<, >, or 2>), and then include the full
absolute path to the file, surrounded in double quotes. Check the boxes to
enable or disable various configurations of redirections.

Settings:
![alt text][edit-scheme settings]


### Edit the cpp file with your `main()` function

Include the following line inside your project's `main()` function, before you
make any reference or use of `argc` or `argv`:

```c++
#include "xcode_redirect.hpp"   // Add near the top of the file with main()

...

int main(int argc, char *argv[]) {
    xcode_redirect(argc, argv);   // Be sure to do this!
    ...

    cin >> my_variable;   // Reads from file instead of keyboard when redirected
    cout << my_result;   // Prints to file instead of screen when redirected
    cerr << my_msg;   // Prints to file instead of screen when redirected
```


[download the file directly]: https://gitlab.umich.edu/eecs281/xcode_redirect/raw/master/xcode_redirect.hpp "xcode_redirect.hpp URL"
[add-files navigator]: images/add-files-_navigator_.png "Add files to project through Project Navigator"
[add-files menu]: images/add-files-_menu_.png "Add files to project through File Menu"
[add-files settings]: images/add-files-settings.png "Add file settings"
[edit-scheme editor]: images/edit-scheme-_editor_.png "Edit project scheme through main editor window interface"
[edit-scheme menu]: images/edit-scheme-_menu_.png "Edit project scheme through Project Menu"
[edit-scheme settings]: images/edit-scheme-settings.png "Edit Arguments Passed On Launch"
