# Contributing Guide
**Status of this document:** Draft

## Table of Contents
1. [Quick Start Guide](#Quick Start Guide)
2. [Code of Conduct](#Code of Conduct)
3. [Code Style](#Code Style)
  1. [Python](#Python)
  2. [Django](#Django)
  3. [Apps](#Apps)
  4. [Models](#Models)
  5. [Forms](#Forms)
  6. [Templates](#Templates)
  7. [URL patterns](#URL patterns)
  8. [Naming conventions](#Naming conventions)

4. [Documentation](#Documentation)
5. [Git](#Git)
  1. [Commits](#Commits)
  2. [Pull-Requests & Patches](#Pull-Requests & Patches)
  3. [Tags](#Tags)
  4. [Bug tracking, features, issues](#Bug tracking, features, issues)
6. [Releases](#Releases)
  1. [Versioning](#Versioning)
  2. [Tags](#Tags)
  3. [Changelog](#Changelog)
  4. [Django version support](#django-version-support)

## Quick Start Guide
Getting started is easy. Just install:

```bash
pip install -r requirements-dev.txt; pre-commit install
```

To make contributing even easier, make sure your editor's or IDE's [EditorConfig] support is enabled.

## Code of Conduct
As contributors and maintainers of this project, and in the interest of fostering an open and welcoming community, we pledge to respect all people who contribute through reporting issues, posting feature requests, updating documentation, submitting pull requests or patches, and other activities.

We are committed to making participation in this project a harassment-free experience for everyone, regardless of level of experience, gender, gender identity and expression, sexual orientation, disability, personal appearance, body size, race, ethnicity, age, religion, or nationality.

Examples of unacceptable behavior by participants include:
- The use of sexualized language or imagery
- Personal attacks
- Trolling or insulting/derogatory comments
- Public or private harassment
- Publishing other's private information, such as physical or electronic addresses, without explicit permission
- Other unethical or unprofessional conduct.

Project maintainers have the right and responsibility to remove, edit, or reject comments, commits, code, wiki edits, issues, and other contributions that are not aligned to this Code of Conduct. By adopting this Code of Conduct, project maintainers commit themselves to fairly and consistently applying these principles to every aspect of managing this project. Project maintainers who do not follow or enforce the Code of Conduct may be permanently removed from the project team.

This code of conduct applies both within project spaces and in public spaces when an individual is representing the project or its community.

Instances of abusive, harassing, or otherwise unacceptable behavior may be reported by opening an issue or contacting one or more of the project maintainers.

This Code of Conduct is adapted from the [Contributor Covenant](http://contributor-covenant.org), version 1.2.0, available at [http://contributor-covenant.org/version/1/2/0/](http://contributor-covenant.org/version/1/2/0/)

## Code Style
### Python
- [pep8]
- [pep20]
- [pep257]
- [pep287]

### Django
We embrace the [django coding style] with the following additions.

#### Apps
Apps should be named according to the system they contain. If there is no system name you may use the plural of the main model's name.

#### Models
Models are defined according to the [django coding style] with the addition of [choices]. Choices are declared right above the corresponding field. The field default is set using a choices attribute.

#### Forms
We declare `ModelForm`s just like we do `Model`s.

#### Templates
Templates are located in the following directory structure: `/{app_name}/templates/{app_name}/`

Every template should be named `{model_name}_{template_name_suffix}` if possible.
Furthermore all templates within the same app should share a common ancestor
called, `base.html` or if possible not extend parent template.
As a result each template should start with `{% extend '{app_name}/base.html' %}`
or not extend at all.

Example:

```
/myapp/templates/myapp/
    ./base.html
    ./customer_create.html
    ./customer_update.html
    ./customer_detail.html
```

##### URL patterns
- All apps should use url **namespaces**, the namespace should be identical to the app name.
- Patterns should be in a separate line than the view and name.
- We do not use view decorators in the url configuration.
- We follow the [django admin][reversing-admin-urls] url pattern, and
- [djangorestframework][drf-routers] url name pattern.

Example:

```python
from . import views

urlpatterns = patterns(
    'customers.views',
    url(r'^customer/$',
     views.CustomerListView.as_view(), name='customer-list'),
    url(r'^customer/create',
     views.CustomerCreateView.as_view(), name='customer-create'),
    url(r'^customer/(?P<pk>\d+)/$',
     views.CustomerDetailView.as_view(), name='customer-detail'),
    url(r'^customer/(?P<pk>\d+)/update',
     views.CustomerUpdateView.as_view(), name='customer-update'),
)
```

##### Naming conventions
Avoid names which does not give additional meaning or are unclear. Some
examples of such names are: Better, Quick, Smart, Clever, Simple, Fast,
Strange, Stupid.

In general one should not use abbreviations and acronyms unless its known by
most programmers. Typical examples for known acronyms are: HTTP, HTML, URL.

The following naming conventions should be used to ensure consistency
throughout all source code. If the names don't make much sense in a given
context other names should be found. Here are some recommendations:

- For file or directory paths use `path`,
- For filename without a path use `file`,
- For directory name without a path use `dir`.
- Use `load`, `save` for complete operations on the file system, for instance
  loading an entire `JSON` file.
- Use `read`, `write` for partial operations of data stream, for instance
  storing 10 bytes to a file.
- Use `fetch`, `store` for remote operations, for instance fetching data from a
  web server or database.
- When adding elements the following naming should be used:
  - Use `add` when adding elements without a specific order.
  - Use `insert` when adding elements in a specific order, for instance at a
    given index or position.
  - Use `append` when adding elements to the end.
  - Use `prepend` when adding elements to the beginning.
- Use `create` for object creation and `generate` for operations that
  generate text, code, SQL etc.
- Use `reset` for resetting elements in the object.
- When removing elements the following naming should be used:
  - Use `remove` when elements are no longer referenced but not actually
    deleted. For instance removing a file path from a list while still leaving
    the file on the file system.
  - Use `delete` when elements are no longer meant to exists. For instance
    unlinking a file from the file system or deleting a database record.
- Short names are advised when their context is very clear. An example is a
  copy() function in a File class which has a source and a destination, it is
  quite clear that in this context we are working with files and can use
  abbreviated forms, `src` and `dest`.  copy( src, dest ) The order of source
  and destination is always source first.
- Some words are different in British English and American English. It is most
  common to use the American spelling and so all words should follow this.
  Some typical names are: initialize, finalize, color, grey.

## Documentation
- [pep257]
- [pep287]

## Git
### Commits
### Pull-Requests & Patches
## Bug tracking, features, issues
## Releases
### Versioning
Versioning happens as defined in [Semantic Versioning 2.0.0](http://semver.org/spec/v2.0.0.html) by Tom Preston-Werner.

Remember, changed or new features are never to be pushed in a bug fix version, but allow people to update without care.

### Tags
Every release is to be tagged with the version number.

Example:
```bash
git tag v2.3.1
git push --tags
```

### Changelog
An overview over all changes in new version should be available at all times and distributed with both source code and binary bundles.
All changes should be listed and grouped by bug fixed, new and changed features. References to tickets are to be added if available to allow user to read up on design decisions.

Example for a `CHANGELOG.md` file:
```Mardown
# v2.3.1 _latest_
- Fixes #1234 -- Nasty bug making the whole thing freeze
- Fixes #1244 -- Yet another issue

# v2.3.0
- Changes #1129 -- Switched important engine
- Adds #459 -- Support for that amazing new feature
- Fixes #1245 -- Yet another issue
```

### Django version support
This project officially support the latest version of Django only. This allows for a more rapid development and reduces code complexity.

People looking for support for an older Django version, may use an older release that supported the Django version in question.

[editorconfig]: examples/.editorconfig
[pep8]: http://legacy.python.org/dev/peps/pep-0008/
[pep20]: http://legacy.python.org/dev/peps/pep-0020/
[pep257]: http://legacy.python.org/dev/peps/pep-0257/
[pep287]: http://legacy.python.org/dev/peps/pep-0287/
[reversing-admin-urls]: https://docs.djangoproject.com/en/dev/ref/contrib/admin/#reversing-admin-urls
[drf-routers]: http://www.django-rest-framework.org/api-guide/routers/
[choices]: https://django-model-utils.readthedocs.org/en/latest/utilities.html#choices
[django coding style]: https://docs.djangoproject.com/en/dev/internals/contributing/writing-code/coding-style/
