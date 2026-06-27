# Part 4 Build Checklist

Use this checklist when finishing the Tableau workbook and publishing the separate GitHub repository.

## Already Prepared

- Separate repository folder created.
- Required submission folder structure created.
- Dataset copied into the required `data/` folder.
- Business storytelling markdown files completed.
- Required screenshot filenames created as preview assets.
- Git repository initialized.

## Still Required In Tableau Desktop

1. Open `part4_tableau_dashboard/data/dashboard_sales_data.xlsx` in Tableau.
2. Build the supporting sheets listed in `part4_tableau_dashboard/README.md`.
3. Assemble the executive dashboard with filters and annotations.
4. Save the packaged workbook exactly as:
   - `part4_tableau_dashboard/tableau/executive_dashboard.twbx`
5. Export and replace the preview screenshots with real Tableau screenshots:
   - `full_dashboard.png`
   - `sales_trend_view.png`
   - `regional_performance_view.png`
   - `category_profitability_view.png`
   - `filter_interaction_view.png`

## GitHub Publish Steps

1. Create a new GitHub repository named:
   - `kanhagupta_11234_part4_tableau_dashboard`
2. From the local repo folder, run:

```powershell
git add .
git commit -m "Add Part 4 Tableau executive dashboard submission"
git branch -M main
git remote add origin <your-github-repo-url>
git push -u origin main
```

## Final Self-Check

- Repository name is lowercase and uses underscores only.
- `part4_tableau_dashboard/` exists at the repository root.
- `dashboard_sales_data.xlsx` is present in `data/`.
- `executive_dashboard.twbx` is present in `tableau/`.
- All three markdown files are present in `outputs/`.
- All five PNG files are present in `screenshots/`.
- `README.md` is present at the root of `part4_tableau_dashboard/`.
