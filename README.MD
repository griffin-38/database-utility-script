Below is a sample **README.md** file you can include in your repository. Adjust any details to suit your specific needs and environment.

---

# DB Reset Script

This repository contains two Bash scripts for resetting a specified database environment. The scripts assume a PostgreSQL setup, but you can modify the logic for other database systems.

## Overview

- **`cleanup_db.sh`**: The main script that handles the overall reset process.  
- **`functions_db.sh`**: A helper script containing the `reset_database` function, which drops and recreates the specified database.

## Prerequisites

1. **Bash** (usually pre-installed on Linux/macOS systems).
2. **PostgreSQL** command-line tools, such as `psql`.
3. Appropriate permissions to drop and create databases (e.g., a user with `CREATE DATABASE` privileges).

Follow these steps prior to executing the script:

1. Create and add a file in your directory: [dbclean]
2. Passwords for psql connections
   - Add ~/.pgpass to the home directory with all passwords for db(s)
3. Update bash_profile with the path to the scripts folder:
   - Run `emacs .bash_profile` then `source .bash_profile`
4. Add path: `export SCRIPT_HOME=/Users/[user.name]/dbclean`


## Usage

1. **Clone the repository** (or download the two script files):
   ```bash
   git clone https://github.com/YourUsername/db-reset-script.git
   cd db-reset-script
   ```

2. **Make the scripts executable** (if they are not already):
   ```bash
   chmod +x cleanup_db.sh
   chmod +x functions_db.sh
   ```

3. **Run the main script** with the name of the database you want to reset:
   ```bash
   ./cleanup_db.sh <database_name>
   ```

   For example:
   ```bash
   ./cleanup_db.sh my_database
   ```

4. **What Happens**:
   - `cleanup_db.sh` sources `functions_db.sh`.
   - The `reset_database` function is called, which drops the existing database and recreates it.
   - You can add optional steps (like migrations or seed data) within the `reset_database` function.

## Customization

- **Database Type**: If you’re using MySQL, Oracle, or another DB, replace PostgreSQL-specific commands in `functions_db.sh` with your preferred database commands.
- **User Permissions**: Ensure your database user has the necessary permissions to drop and create databases.
- **Migrations/Seeding**: If you need to run migrations or seed data, add the relevant commands under the comments in `functions_db.sh`.

## Use with Travis CI

```bash
# Run the following commands in your terminal to make the scripts executable:

chmod +x cleanup_db.sh
chmod +x functions_db.sh

# Replace 'your_db_environment' with the actual 'environment name' and run:

'[ENV=your_db_environment]' ./cleanup_db.sh
'[ENV=waterfront_qa7_db]' ./cleanup_db.sh

# Manual Confirmation 

When you run this script with a command like [ENV=your_db_environment] ./cleanup_db.sh, it will clean the specified database environment, and then wait for user input before exiting.


## Travis CI Integration

This repository includes integration with Travis CI to automate the execution of the database cleanup script. The Travis CI configuration is defined in the [.travis.yml](.travis.yml) file. The script is triggered during specific stages of the CI/CD pipeline.

## Steps to Execute the Cleanup Script in Travis CI

1. Script Details: The main cleanup script is [**cleanup_db.sh**], and it resets a specified database environment using a function from an external file [**functions_db.sh**]. Make sure to customize the script based on your specific database and requirements.

2. Remove Prompt: To execute the cleanup process in the [cleanup_db.sh] file without 'manual confirmation', particularly in CI/CD environments where automation is preferred, you may consider removing the user input prompt if its not needed.

3. Travis CI Configuration: The [.travis.yml](.travis.yml) file in the repository defines the Travis CI configuration. It includes stages and jobs that specify when and how the cleanup script should be executed. Refer to the file for a detailed understanding.

4. Execute Script in Travis CI: To execute the cleanup process in Travis CI, the script is run with a specified environment variable. 

For example:
   
   '[ENV=your_db_environment] ./cleanup_db.sh'
   '[ENV=waterfront_qa7_db] ./cleanup_db.sh'


## Troubleshooting

- **Access Denied or Permission Issues**: Verify that your user has the appropriate privileges and that you’re connecting to the correct database server/host.
- **Command Not Found**: Make sure you have PostgreSQL (or your chosen DB’s client tools) installed and that they are in your system’s `PATH`.

## License

You can choose the license that best fits your project. For example, MIT License:

```
MIT License

Copyright (c) 2020 Omar Miskinyar

Permission is hereby granted, free of charge, to any person obtaining a copy 
of this software and associated documentation files (the "Software"), to deal 
in the Software without restriction, including without limitation the rights 
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell 
copies of the Software, and to permit persons to whom the Software is 
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in 
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR 
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, 
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE 
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER 
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, 
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN 
THE SOFTWARE.

```

---
