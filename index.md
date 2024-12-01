---
layout: default
---

# Analysis of Proposed Amendments of the Constitution between 1787 to 2014
Michael McDonald, Dhruvak Mirani, Olaniyi Salami, Gianfranco Secondi


### Contributions
Michael: contributed to brainstorming in part A, responsible for preprocessing in part B, data exploration in part C and assembling the document in part G

Dhruvak: contributed to brainstorming in part A, did statistical analysis in part C, and wrote the conclusion for part F

Olaniyi: contributed to brainstorming in part A, did statistical analysis in part C, worked on part D, E and the visualization of F

Gianfranco: contributed to brainstorming in part A, did statistical analysis in part C, worked on part D, E and the visualization of F



### Introduction

The objective of this project was to analyze the historical evolution of priorities and perceived problems of the American public. Specifically we wanted to answer the question _can the language and content of proposed amendments reveal the century in which they were proposed?_ Answering this question is important because it will reveal how the issues Americans deemed critical have evolved and how historical context shapes our political and legal discourse.

### Data curation

Our data is a dataset of proposed amendments from the year 1787 to 2014. This dataset provides the title/description of each amendment, the date proposed, the sponsor name, the sponsor state, the Congress number, the congress sessions, the joint resolution chamber and the joint resolution number. 

The dataset comes from the United States government's open data website data.gov, specifically from the National Archives and Records Administration who published the data. The link to the dataset is below

[Link to the dataset](https://catalog.data.gov/dataset/amending-america-proposed-amendments-to-the-united-states-constitution-1787-to-2014)


Now to transform our data to a suitable format for analysis, we first import pandas so we can convert the dataset into a dataframe

```python
import pandas as pd
df = pd.read_csv("proposed_amendments.csv", encoding="ISO-8859-1")
df
```
 <div id="df-c058efc0-f450-421e-ad28-112b02644e44" class="colab-df-container">
    <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>identifier</th>
      <th>source_code</th>
      <th>source_citation</th>
      <th>source_index_number</th>
      <th>title_or_description_from_source</th>
      <th>date_approximation</th>
      <th>year</th>
      <th>month</th>
      <th>day</th>
      <th>congress</th>
      <th>congressional_session</th>
      <th>joint_resolution_chamber</th>
      <th>joint_resolution_number</th>
      <th>sponsor_name</th>
      <th>sponsor_state_or_territory</th>
      <th>committee_of_referral</th>
      <th>last_modified</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>us-nara-amending-america-000001</td>
      <td>A</td>
      <td>Ames, Herman V. The Proposed Amendments to the...</td>
      <td>1</td>
      <td>Reservation of nondelegated powers</td>
      <td>circa</td>
      <td>1788.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2016-02-25T17:29:59.732-05:00</td>
    </tr>
    <tr>
      <th>1</th>
      <td>us-nara-amending-america-000002</td>
      <td>A</td>
      <td>Ames, Herman V. The Proposed Amendments to the...</td>
      <td>2</td>
      <td>Apportionment of Representatives</td>
      <td>circa</td>
      <td>1788.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2016-02-25T17:29:59.732-05:00</td>
    </tr>
    <tr>
      <th>2</th>
      <td>us-nara-amending-america-000003</td>
      <td>A</td>
      <td>Ames, Herman V. The Proposed Amendments to the...</td>
      <td>3</td>
      <td>Restriction on Federal control over election o...</td>
      <td>circa</td>
      <td>1788.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2016-02-25T17:29:59.732-05:00</td>
    </tr>
    <tr>
      <th>3</th>
      <td>us-nara-amending-america-000004</td>
      <td>A</td>
      <td>Ames, Herman V. The Proposed Amendments to the...</td>
      <td>4</td>
      <td>Restriction upon the levying of direct taxes</td>
      <td>circa</td>
      <td>1788.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2016-02-25T17:29:59.732-05:00</td>
    </tr>
    <tr>
      <th>4</th>
      <td>us-nara-amending-america-000005</td>
      <td>A</td>
      <td>Ames, Herman V. The Proposed Amendments to the...</td>
      <td>5</td>
      <td>Commercial monopolies prohibited</td>
      <td>circa</td>
      <td>1788.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2016-02-25T17:29:59.732-05:00</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>11792</th>
      <td>us-nara-amending-america-011793</td>
      <td>G</td>
      <td>United States Congress. Congress.gov: Legislat...</td>
      <td>NaN</td>
      <td>A joint resolution proposing an amendment to t...</td>
      <td>NaN</td>
      <td>2013.0</td>
      <td>6.0</td>
      <td>18.0</td>
      <td>113.0</td>
      <td>NaN</td>
      <td>Senate Joint Resolution</td>
      <td>19.0</td>
      <td>Udall, Tom</td>
      <td>New Mexico</td>
      <td>Judiciary</td>
      <td>2016-02-25T17:29:59.732-05:00</td>
    </tr>
    <tr>
      <th>11793</th>
      <td>us-nara-amending-america-011794</td>
      <td>G</td>
      <td>United States Congress. Congress.gov: Legislat...</td>
      <td>NaN</td>
      <td>A joint resolution proposing a balanced budget...</td>
      <td>NaN</td>
      <td>2013.0</td>
      <td>7.0</td>
      <td>11.0</td>
      <td>113.0</td>
      <td>NaN</td>
      <td>Senate Joint Resolution</td>
      <td>20.0</td>
      <td>Udall, Tom</td>
      <td>New Mexico</td>
      <td>Judiciary</td>
      <td>2016-02-25T17:29:59.732-05:00</td>
    </tr>
    <tr>
      <th>11794</th>
      <td>us-nara-amending-america-011795</td>
      <td>G</td>
      <td>United States Congress. Congress.gov: Legislat...</td>
      <td>NaN</td>
      <td>A joint resolution proposing an amendment to t...</td>
      <td>NaN</td>
      <td>2013.0</td>
      <td>10.0</td>
      <td>11.0</td>
      <td>113.0</td>
      <td>NaN</td>
      <td>Senate Joint Resolution</td>
      <td>25.0</td>
      <td>Paul, Rand</td>
      <td>Kentucky</td>
      <td>Judiciary</td>
      <td>2016-02-25T17:29:59.732-05:00</td>
    </tr>
    <tr>
      <th>11795</th>
      <td>us-nara-amending-america-011796</td>
      <td>G</td>
      <td>United States Congress. Congress.gov: Legislat...</td>
      <td>NaN</td>
      <td>A joint resolution proposing an amendment to t...</td>
      <td>NaN</td>
      <td>2014.0</td>
      <td>3.0</td>
      <td>13.0</td>
      <td>113.0</td>
      <td>NaN</td>
      <td>Senate Joint Resolution</td>
      <td>34.0</td>
      <td>Enzi, Michael</td>
      <td>Wyoming</td>
      <td>Judiciary</td>
      <td>2016-02-25T17:29:59.732-05:00</td>
    </tr>
    <tr>
      <th>11796</th>
      <td>us-nara-amending-america-011797</td>
      <td>G</td>
      <td>United States Congress. Congress.gov: Legislat...</td>
      <td>NaN</td>
      <td>A joint resolution proposing an amendment to t...</td>
      <td>NaN</td>
      <td>2014.0</td>
      <td>6.0</td>
      <td>4.0</td>
      <td>113.0</td>
      <td>NaN</td>
      <td>Senate Joint Resolution</td>
      <td>37.0</td>
      <td>Graham, Lindsey</td>
      <td>South Carolina</td>
      <td>Judiciary</td>
      <td>2016-02-25T17:29:59.732-05:00</td>
    </tr>
  </tbody>
</table>
<p>11797 rows × 17 columns</p>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-c058efc0-f450-421e-ad28-112b02644e44')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960">
    <path d="M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z"/>
  </svg>
    </button>

  <style>
    .colab-df-container {
      display:flex;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    .colab-df-buttons div {
      margin-bottom: 4px;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

    <script>
      const buttonEl =
        document.querySelector('#df-c058efc0-f450-421e-ad28-112b02644e44 button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-c058efc0-f450-421e-ad28-112b02644e44');
        const dataTable =
          await google.colab.kernel.invokeFunction('convertToInteractive',
                                                    [key], {});
        if (!dataTable) return;

        const docLinkHtml = 'Like what you see? Visit the ' +
          '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
          + ' to learn more about interactive tables.';
        element.innerHTML = '';
        dataTable['output_type'] = 'display_data';
        await google.colab.output.renderOutput(dataTable, element);
        const docLink = document.createElement('div');
        docLink.innerHTML = docLinkHtml;
        element.appendChild(docLink);
      }
    </script>
  </div>


<div id="df-a9999aff-3d2b-4f90-a36d-ca2d42d9beec">
  <button class="colab-df-quickchart" onclick="quickchart('df-a9999aff-3d2b-4f90-a36d-ca2d42d9beec')"
            title="Suggest charts"
            style="display:none;">

<svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
     width="24px">
    <g>
        <path d="M19 3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zM9 17H7v-7h2v7zm4 0h-2V7h2v10zm4 0h-2v-4h2v4z"/>
    </g>
</svg>
  </button>

<style>
  .colab-df-quickchart {
      --bg-color: #E8F0FE;
      --fill-color: #1967D2;
      --hover-bg-color: #E2EBFA;
      --hover-fill-color: #174EA6;
      --disabled-fill-color: #AAA;
      --disabled-bg-color: #DDD;
  }

  [theme=dark] .colab-df-quickchart {
      --bg-color: #3B4455;
      --fill-color: #D2E3FC;
      --hover-bg-color: #434B5C;
      --hover-fill-color: #FFFFFF;
      --disabled-bg-color: #3B4455;
      --disabled-fill-color: #666;
  }

  .colab-df-quickchart {
    background-color: var(--bg-color);
    border: none;
    border-radius: 50%;
    cursor: pointer;
    display: none;
    fill: var(--fill-color);
    height: 32px;
    padding: 0;
    width: 32px;
  }

  .colab-df-quickchart:hover {
    background-color: var(--hover-bg-color);
    box-shadow: 0 1px 2px rgba(60, 64, 67, 0.3), 0 1px 3px 1px rgba(60, 64, 67, 0.15);
    fill: var(--button-hover-fill-color);
  }

  .colab-df-quickchart-complete:disabled,
  .colab-df-quickchart-complete:disabled:hover {
    background-color: var(--disabled-bg-color);
    fill: var(--disabled-fill-color);
    box-shadow: none;
  }

  .colab-df-spinner {
    border: 2px solid var(--fill-color);
    border-color: transparent;
    border-bottom-color: var(--fill-color);
    animation:
      spin 1s steps(1) infinite;
  }

  @keyframes spin {
    0% {
      border-color: transparent;
      border-bottom-color: var(--fill-color);
      border-left-color: var(--fill-color);
    }
    20% {
      border-color: transparent;
      border-left-color: var(--fill-color);
      border-top-color: var(--fill-color);
    }
    30% {
      border-color: transparent;
      border-left-color: var(--fill-color);
      border-top-color: var(--fill-color);
      border-right-color: var(--fill-color);
    }
    40% {
      border-color: transparent;
      border-right-color: var(--fill-color);
      border-top-color: var(--fill-color);
    }
    60% {
      border-color: transparent;
      border-right-color: var(--fill-color);
    }
    80% {
      border-color: transparent;
      border-right-color: var(--fill-color);
      border-bottom-color: var(--fill-color);
    }
    90% {
      border-color: transparent;
      border-bottom-color: var(--fill-color);
    }
  }
</style>

  <script>
    async function quickchart(key) {
      const quickchartButtonEl =
        document.querySelector('#' + key + ' button');
      quickchartButtonEl.disabled = true;  // To prevent multiple clicks.
      quickchartButtonEl.classList.add('colab-df-spinner');
      try {
        const charts = await google.colab.kernel.invokeFunction(
            'suggestCharts', [key], {});
      } catch (error) {
        console.error('Error during call to suggestCharts:', error);
      }
      quickchartButtonEl.classList.remove('colab-df-spinner');
      quickchartButtonEl.classList.add('colab-df-quickchart-complete');
    }
    (() => {
      let quickchartButtonEl =
        document.querySelector('#df-a9999aff-3d2b-4f90-a36d-ca2d42d9beec button');
      quickchartButtonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';
    })();
  </script>
</div>

  <div id="id_b7cc7d7e-9cc2-4851-b5fd-dce7d2c4c7fd">
    <style>
      .colab-df-generate {
        background-color: #E8F0FE;
        border: none;
        border-radius: 50%;
        cursor: pointer;
        display: none;
        fill: #1967D2;
        height: 32px;
        padding: 0 0 0 0;
        width: 32px;
      }

      .colab-df-generate:hover {
        background-color: #E2EBFA;
        box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
        fill: #174EA6;
      }

      [theme=dark] .colab-df-generate {
        background-color: #3B4455;
        fill: #D2E3FC;
      }

      [theme=dark] .colab-df-generate:hover {
        background-color: #434B5C;
        box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
        filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
        fill: #FFFFFF;
      }
    </style>
    <button class="colab-df-generate" onclick="generateWithVariable('df')"
            title="Generate code using this dataframe."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M7,19H8.4L18.45,9,17,7.55,7,17.6ZM5,21V16.75L18.45,3.32a2,2,0,0,1,2.83,0l1.4,1.43a1.91,1.91,0,0,1,.58,1.4,1.91,1.91,0,0,1-.58,1.4L9.25,21ZM18.45,9,17,7.55Zm-12,3A5.31,5.31,0,0,0,4.9,8.1,5.31,5.31,0,0,0,1,6.5,5.31,5.31,0,0,0,4.9,4.9,5.31,5.31,0,0,0,6.5,1,5.31,5.31,0,0,0,8.1,4.9,5.31,5.31,0,0,0,12,6.5,5.46,5.46,0,0,0,6.5,12Z"/>
  </svg>
    </button>
    <script>
      (() => {
      const buttonEl =
        document.querySelector('#id_b7cc7d7e-9cc2-4851-b5fd-dce7d2c4c7fd button.colab-df-generate');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      buttonEl.onclick = () => {
        google.colab.notebook.generateWithVariable('df');
      }
      })();
    </script>
  </div>

    </div>
  </div>







  


Text can be **bold**, _italic_, or ~~strikethrough~~.

[Link to another page](./another-page.html).

There should be whitespace between paragraphs.

There should be whitespace between paragraphs. We recommend including a README, or a file with information about your project.

# Header 1

This is a normal paragraph following a header. GitHub is a code hosting platform for version control and collaboration. It lets you and others work together on projects from anywhere.

## Header 2

> This is a blockquote following a header.
>
> When something is important enough, you do it even if the odds are not in your favor.

### Header 3

```js
// Javascript code with syntax highlighting.
var fun = function lang(l) {
  dateformat.i18n = require('./lang/' + l)
  return true;
}
```

```ruby
# Ruby code with syntax highlighting
GitHubPages::Dependencies.gems.each do |gem, version|
  s.add_dependency(gem, "= #{version}")
end
```

#### Header 4

*   This is an unordered list following a header.
*   This is an unordered list following a header.
*   This is an unordered list following a header.

##### Header 5

1.  This is an ordered list following a header.
2.  This is an ordered list following a header.
3.  This is an ordered list following a header.

###### Header 6

| head1        | head two          | three |
|:-------------|:------------------|:------|
| ok           | good swedish fish | nice  |
| out of stock | good and plenty   | nice  |
| ok           | good `oreos`      | hmm   |
| ok           | good `zoute` drop | yumm  |

### There's a horizontal rule below this.

* * *

### Here is an unordered list:

*   Item foo
*   Item bar
*   Item baz
*   Item zip

### And an ordered list:

1.  Item one
1.  Item two
1.  Item three
1.  Item four

### And a nested list:

- level 1 item
  - level 2 item
  - level 2 item
    - level 3 item
    - level 3 item
- level 1 item
  - level 2 item
  - level 2 item
  - level 2 item
- level 1 item
  - level 2 item
  - level 2 item
- level 1 item

### Small image

![Octocat](https://github.githubassets.com/images/icons/emoji/octocat.png)

### Large image

![Branching](https://guides.github.com/activities/hello-world/branching.png)


### Definition lists can be used with HTML syntax.

<dl>
<dt>Name</dt>
<dd>Godzilla</dd>
<dt>Born</dt>
<dd>1952</dd>
<dt>Birthplace</dt>
<dd>Japan</dd>
<dt>Color</dt>
<dd>Green</dd>
</dl>

```
Long, single-line code blocks should not wrap. They should horizontally scroll if they are too long. This line should be long enough to demonstrate this.
```

```
The final element.
```