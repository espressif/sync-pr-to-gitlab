We welcome contributions! To contribute to this repository, please read these instructions:

- [Project Organization](#project-organization)
- [Code and Testing](#code-and-testing)
- [Documentation and Maintenance](#documentation-and-maintenance)
- [Development and Local Testing](#development-and-local-testing)
  - [Testing](#testing)

---

## Project Organization

- **Project Configuration:** The setup for both production and development dependencies is outlined in the `pyproject.toml` file. This centralized approach simplifies dependency management.

- **Automatic `requirements.txt`:** Changes to dependencies are automatically reflected in the `requirements.txt` file, derived from `pyproject.toml`. Direct modifications should be avoided; instead, update `pyproject.toml`.

- **Automatic `requirements.txt`:** Changes to dependencies are automatically reflected in the `requirements.txt` file, derived from `pyproject.toml`. Direct modifications to `requirements.txt` should be avoided; instead, update `pyproject.toml`. The auto-generated `requirements.txt` is used for creating a Docker image, ensuring that dependency changes are locked into your containerized environment.


- **Commit Standard:** Adherence to the Espressif standard for Conventional Commits ensures consistency in commit messages. Tools like pre-commit hooks and the integrated PR linter DangerJS assist in formatting commit messages appropriately, a key factor for `commitizen` to auto-generate the changelog.

## Code and Testing

- **Code Style and Structure:**

  - **Pre-Commit Hooks:** Install pre-commit hooks in this repository using the `pre-commit install` command.

  - **Readable Code Structure:** Structure your code in a readable manner. The main logic should be in the default rule function, with implementation details in helper functions. Avoid nested `if` statements and unnecessary `else` statements to maintain code clarity and simplicity.

  - **Remove Debug Statements:** Remove any development debug statements from your files.

## Documentation and Maintenance

- **Changelog:** `CHANGELOG.md` is generated automatically by `commitizen` from commit messages. Not need to update `CHANGELOG.md` manually. Focus on informative and clear commit messages which end in the release notes.

- **Documentation:** Regularly check and update the documentation to keep it current.

- **PR Descriptions and Documentation:** When contributing, describe all changes or new features in the PR (Pull Request) description as well as in the documentation. When changing the style to the output style, attach a thumbnail after the change.

## Development and Local Testing

1. **Clone the Project**

- Clone the repository to your local machine using:

  ```sh
  git clone <project_clone_url>
  ```

2. **Set Up Development Environment:**

- Create and activate a virtual environment:

  ```sh
  python -m venv venv && source ./venv/bin/activate
  ```

  or:

  ```sh
  virtualenv venv && source ./venv/bin/activate
  ```

- Install the project and development dependencies:
  ```sh
  pip install -e '.[dev]'
  ```

### Testing
For testing use our GitHub project [espressif/actions-internal-test](https://github.com/espressif/actions-internal-test).

During the testing phase, it might be necessary to bypass certain checks that are only relevant for the production environment.

You can do this by commenting out specific lines in the python script within the `main()` function. Here's how:

1. **Bypass Repository Check**: Temporarily disable the check that ensures the script is running within an Espressif repository. This allows you to run tests in a forked or local version of the repository without errors.

    ```py
    # if not os.environ['GITHUB_REPOSITORY'].startswith('espressif/'):  # Comment out for testing
    #     print('Not an Espressif repo!')
    #     return
    ```

2. **Repository Name Placeholder**: For testing purposes, you might need to simulate actions against a specific repository's data. Comment out the line fetching the repository's full name to avoid conflicts or errors during this phase.

    ```py
    # repo_fullname = event['repository']['full_name']  # Comment out for testing
    ```

By commenting out these lines, you'll be able to run your tests in a more controlled and isolated manner, simulating different conditions without affecting the actual repository or workflow.

---

👏**Thank you for your contributions.**
