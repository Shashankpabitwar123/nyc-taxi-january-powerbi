# GitHub Publishing Checklist

The report documentation is ready locally. Publishing it requires a GitHub
repository and an authenticated GitHub account.

## One-time setup

```bash
gh auth login -h github.com
```

Create an empty GitHub repository, for example:

```text
nyc-taxi-january-powerbi
```

Then, from the folder containing this project:

```bash
git init -b main
git add nyc-taxi-january-powerbi
git commit -m "Document January NYC Taxi Power BI project"
git remote add origin https://github.com/<your-username>/nyc-taxi-january-powerbi.git
git push -u origin main
```

Before pushing, confirm that the repository contains documentation and
presentation artifacts only. Never add Azure access keys, Power BI tokens, the
`.pbix` file if it contains private connection details, or the full raw trip
Parquet file.

