# Increment Semantic Version

This is a GitHub action to bump a given semantic version, depending on a given version fragment.
This is largly based on christian-draeger/increment-semantic-version
but with the ability to control the version and prerelease parts separately

## Inputs

### `current-version`

**Required** The current semantic version you want to increment. (e.g. 3.12.5)

### `increment-version-fragment`

**Required** The versions fragment you want to increment.

Possible options are **[ NONE | MAJOR | MINOR | PATCH ]**

### `prerelease-fragment`

**Required** The prerelease fragment you want to remove increment.

Possible options are **[ REMOVE | ALPHA | BETA | RC ]**

Note that a value of REMOVE will remove any prerelease fragment

## Outputs

### `updated-version`

The incremented version.

## Example usage

### Moving from release to new Minor Alpha

    - name: Bump release version
      id: bump_version
      uses: cookbenjamin/update-version@v1.0.1
      with:
        current-version: '2.11.7'
        increment-version-fragment: 'MINOR'
        prerelease-fragment: 'ALPHA'
    - name: Do something with your bumped release version
      run: echo ${{ steps.bump_version.outputs.updated-version }}
      # will print 2.12.0-alpha1

### Moving from beta to production

    - name: Bump release version
      id: bump_version
      uses: cookbenjamin/update-version@v1.0.1
      with:
        current-version: '2.11.7-beta3'
        increment-version-fragment: 'NONE'
        prerelease-fragment: 'REMOVE'
    - name: Do something with your bumped release version
      run: echo ${{ steps.bump_version.outputs.updated-version }}
      # will print 2.11.7

## input / output Examples

| increment-version-fragment | prerelease-fragment  | current-version | output        |
| ----------------           | -------------------- | --------------- | ------------- |
| MAJOR                      | ALPHA                | 2.11.7-alpha1   | 3.0.0-alpha1  |
| MAJOR                      | BETA                 | 2.11.7          | 3.0.0-beta1   |
| MAJOR                      | RC                   | 2.11.7-alpha3   | 3.0.0-rc1     |
| MAJOR                      | REMOVE               | 2.11.7-alpha3   | 3.0.0         |
| MINOR                      | ALPHA                | 2.11.7          | 2.12.0-alpha1 |
| MINOR                      | REMOVE               | 2.11.7-alpha3   | 2.12.0        |
| PATCH                      | REMOVE               | 2.11.7          | 2.11.8        |
| PATCH                      | BETA                 | 2.11.7-beta3    | 2.11.8-beta1  |
| PATCH                      | RC                   | 2.11.7          | 2.11.8-rc1    |
| PATCH                      | REMOVE               | 2.11.7-alpha3   | 2.11.8        |
| NONE                       | ALPHA                | 2.11.7          | 2.11.7-alpha1 |
| NONE                       | ALPHA                | 2.11.7-alpha3   | 2.11.7-alpha4 |
| NONE                       | REMOVE               | 2.11.7-alpha4   | 2.11.7        |

# License
The scripts and documentation in this project are released under the [MIT License](LICENSE)
