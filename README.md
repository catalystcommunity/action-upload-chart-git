<!-- start title -->

# GitHub Action:Upload a released helm chart to a git helm charts repository

<!-- end title -->
<!-- start description -->

Extracts a helm chart from a release, adds it to a git helm repository, then reindexes the repository. This action is designed to be run on a release trigger, and to extract a packaged chart in .tgz format from a .tgz file such as chart.tgz.

<!-- end description -->
<!-- start contents -->
<!-- end contents -->
<!-- start usage -->

```yaml
- uses: catalystcommunity/action-upload-chart-git@undefined
  with:
    # Github token to use, must specify a PAT so that the action can clone the charts
    # repo and push changes to it
    token: ""

    # Release tag to fetch chart from
    # Default: ${{ github.event.release.tag_name }}
    tag: ""

    # Release asset label to scan for. Release assets are scanned by lower casing the
    # label and using a jq contains() check. The default value is `helm chart`, if
    # your release assets are labeled differently, specify your label here
    # Default: helm chart
    release-asset-label-contains: ""

    # The git repository to upload the chart to
    # Default: ${{ github.repository_owner }}/charts
    chart-repository: ""

    # The git repository ref to push the chart to
    # Default: main
    chart-repository-ref: ""
```

<!-- end usage -->
<!-- start inputs -->

| **Input**                          | **Description**                                                                                                                                                                                                                   |               **Default**               | **Required** |
| :--------------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------: | :----------: |
| **`token`**                        | Github token to use, must specify a PAT so that the action can clone the charts repo and push changes to it                                                                                                                       |                                         |   **true**   |
| **`tag`**                          | Release tag to fetch chart from                                                                                                                                                                                                   | `${{ github.event.release.tag_name }}`  |  **false**   |
| **`release-asset-label-contains`** | Release asset label to scan for. Release assets are scanned by lower casing the label and using a jq contains() check. The default value is `helm chart`, if your release assets are labeled differently, specify your label here |              `helm chart`               |  **false**   |
| **`chart-repository`**             | The git repository to upload the chart to                                                                                                                                                                                         | `${{ github.repository_owner }}/charts` |  **false**   |
| **`chart-repository-ref`**         | The git repository ref to push the chart to                                                                                                                                                                                       |                 `main`                  |  **false**   |

<!-- end inputs -->
<!-- start outputs -->

| **Output**      | **Description** | **Default** | **Required** |
| :-------------- | :-------------- | ----------- | ------------ |
| `random-number` | Random number   |             |              |

<!-- end outputs -->
<!-- start examples -->

### Example usage

```yaml
name: Upload Released Chart
on:
  release:
    types:
      - published
jobs:
  upload-chart-git:
    runs-on: ubuntu-latest
    steps:
      - name: Dump Context
        uses: crazy-max/ghaction-dump-context@v1
      - name: Push Chart
        uses: catalystcommunity/action-upload-chart-git@v1
        with:
          token: ${{ secrets.AUTOMATION_PAT }}
```

<!-- end examples -->
<!-- start [.github/ghdocs/examples/] -->
<!-- end [.github/ghdocs/examples/] -->
