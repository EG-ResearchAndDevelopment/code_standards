# 1. Code Organisation

D.R.Y. Code (Don’t Repeat Yourself). If you find yourself writing the same code in multiple places, you should organize it into a function or class that can be reused more efficiently while also reducing the probability for errors.


## Python Project File Structure

The structure is flexible but should follow the following overall structure. The project root directory should be named after the project itself, and should be the git repo root directory:

* `{project_root}` (name of the project)
   * `src`
        * **`notebooks`**
        * *`(tests)`*
        * *`(models)`* - not mandatory but highly recomended for more complex projects
        * *`(resources)`* - not mandatory but highly recomended for more complex projects
        * **`data`**
        * **`main.py`** - file where the program runs the entire process
        * **`utils.py`**
        * `(ui)`
            * `canvas`
            * `dashboard`
    * `(ui)`
        * `resources`
    * `(doc)` - not mandatory but highly recomended for more complex projects
        * ...
    * **`README.md`**
    * `LICENSE`
    * **`.gitignore`**
    * **`requirements.txt`**
    * `(setup.py)`

**The `()` brackets indicate that the folder/file is not mandatory, but highly recommended for more complex projects. The **bold** text indicates that the folder/file is mandatory.**

### 2. Directory Details

#### 2.1. project_root

All files that are part of the project. The directory should be named after the project itself, and should be the git repo root directory.

#### 2.2. src
--------
All python source modules, separated into packages where there is shared functionality.

#### 2.3. UI
-------
All of the .ui interface files should be generated from the UI designer of choice. The .ui files should be stored in the 'ui' folder, and the .py files should be stored in the 'ui' folder as well. The 'resources' folder should contain all of the resources used by the UI (e.g. images, icons, etc.).

#### 2.4. doc
--------
All of the documentation generated for this project. Within it are two subfolders, 'api' and 'guide'. 'api' contains API documentation (i.e. docs culled from sources), whereas the 'guide' folder contains our main documentation guide.

### 3. Template to use for new python project

The template project can be found [here](
    https://github.com/EG-ResearchAndDevelopment/new_project_template)

### 4. References to style guides

* [Google Python Style Guide](https://google.github.io/styleguide/pyguide.html)