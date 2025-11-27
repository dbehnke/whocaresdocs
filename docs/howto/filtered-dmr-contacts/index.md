# Filtered DMR Contacts

This guide explains how to get the latest filtered DMR contact list for your radio. We support Baofeng DM-32UV, Anytone, and OpenGD77 formats.

## Why Filter?

The purpose of this tool is to only include active operators instead of the entire global DMR database. This helps to:

- **Reduce Storage Usage:** Many radios have limited contact storage.
- **Speed Up Updates:** Writing a smaller contact list to the radio is significantly faster.
- **Improve Relevance:** You only have contacts for people who have been active recently.

## Download Latest Contacts

The contact list is generated and updated periodically. Since Brandmeister doesn't have an API to get the "Last Heard" data, a human has to use the Brandmeister "Last Heard" CSV export and feed it into our contact filter tool and make a release.

You can download the latest version from the releases page of our contact filter tool. Look for the file corresponding to your radio:

- **Baofeng DM-32UV:** `baofeng-dm32uv_Contacts_<TIMESTAMP>.csv`
- **Anytone:** `anytone_Contacts_<TIMESTAMP>.csv`
- **OpenGD77:** `opengd77_Contacts_<TIMESTAMP>.csv`

[Download Latest Contacts](https://github.com/dbehnke/contactfilter/releases)

## Build it Yourself

If you prefer to generate the contact list yourself or customize the filtering options, you can use our open-source tool.

### Prerequisites

- [Go](https://go.dev/dl/) (version 1.25 or later)
- A Brandmeister "Last Heard" CSV export (optional, for merging active contacts)

### Instructions

1. **Clone the repository:**

    ```bash
    git clone https://github.com/dbehnke/contactfilter.git
    cd contactfilter
    ```

2. **Build the tool:**

    ```bash
    go build -o contactfilter
    ```

3. **Run the generation script:**
    We provide a helper script to automate the process. Ensure you have your `bm_contacts.csv` in the directory if you want to merge active contacts.

    ```bash
    ./generate_local.sh
    ```

    This will download the latest RadioID database, merge it with your Brandmeister data (if available), filter by country, and generate CSV files for all supported radios.

    You can also run the tool manually to specify a particular format:

    ```bash
    ./contactfilter --input-csv bm_contacts.csv --filter-file countries.txt --output-csv my_contacts.csv --radio anytone --merge
    ```

    Supported values for `--radio` are:

    - `baofeng-dm32uv` (Default)
    - `anytone`
    - `opengd77`
    - `db25d`

For more detailed usage instructions and options, please refer to the [project README](https://github.com/dbehnke/contactfilter/blob/main/README.md).
