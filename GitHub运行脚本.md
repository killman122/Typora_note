在GitHub中，你可以通过使用GitHub Secrets 和 GitHub Actions 来向 Python 文件中添加 Cookie。GitHub Secrets 允许你安全地存储和管理敏感信息，如 API 密钥、密码和其他凭据。然后，GitHub Actions 可以访问这些 Secrets 并将它们传递给你的 Python 脚本。

以下是如何在 GitHub 中通过外部的 YAML 文件向 Python 文件中添加 Cookie 的步骤：

1. **准备配置文件：** 首先，你需要创建一个 YAML 文件（例如，`config.yml`），用于存储你的 Cookie 值。

   ```
   yamlCopy code# config.yml
   cookie: YOUR_COOKIE_VALUE
   ```

2. **在 GitHub 中添加 Secrets：** 在你的 GitHub 仓库中，转到 "Settings"（设置）选项卡，然后选择 "Secrets"（秘密）。

3. **添加一个新的 Secret：** 在 Secrets 页面中，点击 "New repository secret"（新建仓库秘密）按钮。

4. **设置 Secret 的名称和值：** 输入一个名称（例如，`MY_COOKIE_SECRET`）并将该名称关联到步骤1中的配置文件中的 Cookie 值（`YOUR_COOKIE_VALUE`）。保存 Secret。

5. **配置 GitHub Actions：** 在你的 GitHub 仓库中，创建一个存放 Python 脚本的目录（例如，`scripts`）。

6. **编写 GitHub Actions Workflow 文件：** 在存放 Python 脚本的目录中，创建一个名为 `main.yml` 的文件，用于定义 GitHub Actions 的 Workflow。

   ```
   yamlCopy codename: My Python Script
   
   on:
     push:
       branches:
         - main
     schedule:
       - cron: '0 0 * * *' # 用于每天UTC时间00:00运行脚本，你可以根据需要调整时间
   
   jobs:
     run_script:
       runs-on: ubuntu-latest
   
       steps:
       - name: Checkout repository
         uses: actions/checkout@v2
   
       - name: Set up Python
         uses: actions/setup-python@v2
         with:
           python-version: '3.x' # 替换成你的Python版本
   
       - name: Install dependencies
         run: pip install requests
   
       - name: Run Python script
         env:
           MY_COOKIE: ${{ secrets.MY_COOKIE_SECRET }} # 传递Secret的值给环境变量MY_COOKIE
         run: python scripts/your_python_script.py
   ```

   在上面的示例中，我们设置了两个触发条件：`push`（代码推送）和 `schedule`（定时运行）。定时运行的 cron 表达式可以根据你的需求进行调整，上面的示例是每天UTC时间的00:00运行脚本。

7. **编写 Python 脚本：** 在刚刚创建的存放 Python 脚本的目录中，编写你的 Python 脚本（例如，`your_python_script.py`）。

   ```
   import os
   
   cookie = os.environ.get('MY_COOKIE')
   # 在这里使用cookie变量执行你的操作
   ```

在上述步骤中，GitHub Actions 会在定时运行或代码推送时触发 Workflow。它将检出仓库，安装 Python 和依赖项，然后通过环境变量 `MY_COOKIE` 传递你的 Cookie 值给你的 Python 脚本。你的 Python 脚本可以通过 `os.environ.get()` 方法获取 Cookie 值并在脚本中使用。同时，你的 Cookie 值是安全存储在 GitHub Secrets 中的，不会暴露在公共代码中。



以上是setting中secret中设置cookie并使用



如果你想要在 GitHub Actions 中读取 `config.yml` 文件中的值，并将其传递给 Python 脚本，你可以考虑使用以下方法：

1. 在 GitHub Actions 的工作流程中使用 `actions/checkout` action，将仓库的代码和 `config.yml` 文件检出到工作目录中。
2. 使用适当的方法读取 `config.yml` 文件，例如使用 Python 的 `open` 函数来读取文件内容，并解析出你需要的配置值。
3. 将从 `config.yml` 文件中读取的值存储在 GitHub Actions 的环境变量中。
4. 将环境变量传递给 Python 脚本，让脚本可以访问这些环境变量中的值。

下面是一个示例的 GitHub Actions 工作流程，展示了如何实现上述步骤：

```
yamlCopy codename: Your Workflow

on:
  push:
    branches:
      - main

jobs:
  your_job:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v2

      - name: Read config.yml and set environment variables
        run: |
          # 读取 config.yml 文件中的值，并设置为环境变量
          COOKIE_VALUE=$(cat path/to/config.yml | grep 'cookie:' | awk '{print $2}')
          echo "COOKIE_VALUE=${COOKIE_VALUE}" >> $GITHUB_ENV

      - name: Set up Python
        uses: actions/setup-python@v2
        with:
          python-version: 3.x

      - name: Install dependencies
        run: pip install requests

      - name: Run Python script
        env:
          COOKIE_VALUE: ${{ env.COOKIE_VALUE }}  # 将环境变量传递给 Python 脚本
        run: python your_script.py
```

在这个示例中，我们使用 `grep` 和 `awk` 命令来提取 `config.yml` 文件中的 `cookie` 值，并将其存储在名为 `COOKIE_VALUE` 的环境变量中。然后，我们在运行 Python 脚本时，将这个环境变量传递给脚本，使得脚本可以访问这个值。

请注意，这只是一个简单示例，并假设 `config.yml` 文件的内容格式是简单的。实际上，读取配置文件的方法可能因文件格式和内容结构而异。你需要根据你的实际情况来调整代码，确保能正确读取配置文件中的值并传递给 Python 脚本。