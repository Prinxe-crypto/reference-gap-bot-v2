name: Reference Gap Bot

on:
  schedule:
    - cron: '*/15 * * * *'
  workflow_dispatch:

jobs:
  run-bot:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-python@v5
        with:
          python-version: '3.11'
      - run: pip install requests pandas
      - run: python paper_trade_logic.py
      - run: |
          git config user.name "github-actions"
          git config user.email "actions@github.com"
          touch open_positions.csv closed_positions.csv
          git add open_positions.csv closed_positions.csv
          git diff --staged --quiet || git commit -m "Update positions"
          git push
