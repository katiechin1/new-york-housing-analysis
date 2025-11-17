# Data Audit — NY Housing Dataset

## Dataset Overview
- Source: [New York Housing Data - Kaggle](https://www.kaggle.com/datasets/shreyapande0/nyc-affordable-housing-production)
- Rows: ~3,000 listings
- Columns: 17
- Coverage: NYC — (Manhattan, Brooklyn, Queens, Bronx, Staten Island)
- Granularity: one record = one property listing

## Column Summary
| Column | Description | Notes |
|---|---|---|
| TYPE | Listing type (e.g., Condo, Co-op, House) | Cleaned and grouped |
| PRICE | Listing price (USD) | Converted to numeric; trimmed top 1% |
| BEDS | Bedrooms | Converted to numeric |
| BATH | Bathrooms | Cast to integer |
| PROPERTYSQFT | Square footage | Filtered > 0 |
| STATE | City + state + ZIP | Used for borough mapping |
| BOROUGH | Derived location | Mapped to five boroughs |
| LATITUDE / LONGITUDE | Coordinates | Optional for mapping |

## Data Quality Checks
- Minimal missing values (< 3%) handled via imputation/removal
- Outliers > 99th percentile in PRICE removed
- PROPERTYSQFT ≤ 0 dropped
- Duplicate addresses removed
- Text columns standardized for spacing and case

## Property Type Cleanup
- Removed inactive or nonsensical types (Coming Soon, Sold, Pending, Foreclosure, Auction, Off Market, Mobile House).
- Removed redundant suffixes (for sale, by owner).
- Grouped similar labels into: Condo, Co-op, Townhouse, House, Multi-Family.

## Derived Fields
| New Field | Formula | Purpose |
|---|---|---|
| price_per_sqft | PRICE / PROPERTYSQFT | Compare affordability |
| price_range | Bins via pd.cut() | Visualize price segments |
| type_grouped | Cleaned TYPE | Simplify visual categories
