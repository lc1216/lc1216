name: Metrics
on:
  schedule:
    - cron: "0 */6 * * *" # 每6小时自动统计一次
  workflow_dispatch: # 允许手动点击运行

jobs:
  github-metrics:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      - name: Generate Core Metrics (Default White Theme)
        uses: lowlighter/metrics@latest
        with:
          token: ${{ secrets.TOKEN }} # 读取你仓库里的密钥
          user: lc1216
          template: classic
          base: header, activity, community, repositories, metadata # 统计项目总数和基础数据
          config_timezone: Asia/Shanghai
          
          # 核心语言分类统计（开启后会自动统计你所有公开+私有仓库的语言占比）
          plugin_languages: yes
          plugin_languages_ignored: html, css, tex, less, sass, scss # 过滤掉非核心标记语言
          plugin_languages_details: bytes-size, percentage
          plugin_languages_limit: 8
