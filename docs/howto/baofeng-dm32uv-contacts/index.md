# Baofeng DM-32UV Contacts

This guide explains how to get the latest DMR contact list for your Baofeng DM-32UV radio.

## Download Latest Contacts

The contact list is automatically generated and updated daily. You can download the latest version from the releases page of our contact filter tool.

[Download Latest Contacts](https://github.com/dbehnke/contactfilter/releases)

Look for the file named `Baofeng_DM-32UV_Contacts_<TIMESTAMP>.csv` in the latest release assets.

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

    This will download the latest RadioID database, merge it with your Brandmeister data (if available), filter by country, and generate a new CSV file ready for import into your radio.

For more detailed usage instructions and options, please refer to the [project README](https://github.com/dbehnke/contactfilter/blob/main/README.md).
