# Data Cleaning Guide
## Logistics Data Integrity & Optimization Project

---

## PART 1: Step-by-Step Excel Data Cleaning Guide ENJOYY!!

The following numbered steps describe exactly how to clean `raw_data.csv` using only standard Microsoft Excel features — no coding required.

---

### Step 1 — Open and Inspect the Raw Data

1. Open `raw_data.csv` in Microsoft Excel.
2. Press **Ctrl + End** to find the last used cell and confirm the dataset has 15 rows (plus 1 header row).
3. Scroll through the data visually and note any obvious inconsistencies in the `Ship_Date`, `Carrier`, and `Shipping_Cost` columns.

---

### Step 2 — Remove the Duplicate Row

1. Click any cell inside the data range.
2. Go to the **Data** tab → click **Remove Duplicates**.
3. In the dialog box, ensure all columns are checked, then click **OK**.
4. Excel will report that 1 duplicate was found and removed (Shipment ID SH-1004, Row 11).
5. You should now have 14 unique rows.

> **Verification:** Use `=COUNTIF(A:A, A2)` in a helper column to confirm no Shipment_ID appears more than once.

---

### Step 3 — Standardize Date Formats with Power Query

1. Go to the **Data** tab → click **Get & Transform Data → From Text/CSV** and reload `raw_data.csv`, or use the existing table.
2. In **Power Query Editor**, select the `Ship_Date` column.
3. Go to **Transform** → **Data Type** → select **Date**.
4. Power Query will parse all three date formats (`YYYY-MM-DD`, `MM/DD/YYYY`, `Mon DD YYYY`) and convert them to a single unified date.
5. Click **Close & Load** to return the cleaned data to your spreadsheet.
6. Right-click the `Ship_Date` column → **Format Cells** → **Date** → choose format `YYYY-MM-DD` to display consistently.

> **Alternative (without Power Query):** Use Find & Replace to manually reformat the inconsistent entries (e.g., change `01/16/2024` to `2024-01-16` and `Jan 19 2024` to `2024-01-19`).

---

### Step 4 — Fix Inconsistent Carrier Name Casing

1. Press **Ctrl + H** to open the **Find & Replace** dialog.
2. Perform the following replacements one at a time:
   - Find `fedex` → Replace with `FedEx`
   - Find `FEDEX` → Replace with `FedEx`
   - Find `ups` → Replace with `UPS`
3. Click **Replace All** for each entry and confirm the replacements.
4. Scan the column to confirm all carrier names now use consistent title-case formatting.

> **Tip:** You can also use `=PROPER(C2)` in a helper column to auto-capitalize entries, then paste the values back using **Paste Special → Values Only**.

---

### Step 5 — Fill in the Missing Carrier Name

1. Press **Ctrl + G** → click **Special** → select **Blanks** → click **OK**.
2. Excel will highlight all empty cells. The blank in the `Carrier` column (Row 6, SH-1005) will be selected.
3. Type `Unknown` and press **Enter** to fill in the missing value.
4. Document this in a separate log or comment so the operations team can follow up with the source record.

---

### Step 6 — Replace Invalid "N/A" Values in Shipping Cost

1. Click the header of the `Shipping_Cost` column to select it.
2. Press **Ctrl + H** to open **Find & Replace**.
3. In the **Find what** field, type `N/A`.
4. In the **Replace with** field, type `0.00`.
5. Click **Replace All**. This corrects the two invalid text entries in SH-1003 and SH-1011.
6. Reformat the column: select it, right-click → **Format Cells** → **Number** → **Currency** (or 2 decimal places).

---

### Step 7 — Apply Data Validation to Prevent Future Errors

1. Select the entire `Shipping_Cost` column (excluding the header).
2. Go to **Data** tab → **Data Validation**.
3. Under **Allow**, select **Decimal**. Set **Minimum** to `0`.
4. In the **Error Alert** tab, set the title to `Invalid Entry` and message to `Shipping cost must be a positive number.`
5. Click **OK**. This prevents future `N/A` or text entries in that column.

---

### Step 8 — Run a Final Audit with Conditional Formatting

1. Select the entire data range (A1:G15).
2. Go to **Home** tab → **Conditional Formatting** → **New Rule**.
3. Select **Format only cells that contain** → choose **Blanks** → set the fill color to red.
4. Any remaining empty cells will be highlighted, making the final audit instant.

---

### Step 9 — Validate with a PivotTable

1. Click any cell in your cleaned data.
2. Go to **Insert** → **PivotTable** → click **OK**.
3. Drag `Carrier` to the **Rows** area.
4. Drag `Shipping_Cost` to the **Values** area (set to **Sum**).
5. Drag `Shipment_ID` to the **Values** area (set to **Count**).
6. Review the totals to confirm they match expected record counts and flag any carrier with unusually high or low cost averages.

