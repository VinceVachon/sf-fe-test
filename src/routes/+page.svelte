<!-- Index -->
<script lang="ts">
</script>

<h1>Welcome</h1>
<p>
  Build a job board that displays the latest job postings fetched from the
  Hacker News API, with each posting displaying the job <strong>title</strong>,
  <strong>poster</strong>, and <strong>date posted</strong>.
</p>

<ul>
  <li>
    The page should show 6 jobs on initial load with a button to load more
    postings.
  </li>
  <li>
    Clicking on the "Load more" button will load the next page of 6 postings.
    The button does not appear if there aren't any more postings to load.
  </li>
  <li>
    If there's a url field returned for the job details, make the job title a
    link that opens the job details page in a new window when clicked.
  </li>
  <li>The timestamp can be formatted in any way you like.</li>
</ul>

<h2>Api</h2>
<p>Hacker News has a public API to fetch jobs by Y Combinator companies:</p>

<h3>Job Stories</h3>
<p>Fetches a <strong>list of job posting</strong> IDs.</p>

<ul>
  <li>URL: https://hacker-news.firebaseio.com/v0/jobstories.json</li>
  <li>HTTP Method: GET</li>
  <li>Content Type: json</li>
</ul>

<p>Sample response:</p>
<pre>
    <code>
    [35908337, 35904973, 35900922, 35893439, 35890114, 35880345, ...]
    </code>
</pre>

<h3>Job Details</h3>
<p>Fetches job posting <strong>details</strong> given its ID.</p>

<ul>
  <li>URL: https://hacker-news.firebaseio.com/v0/item/{`id`}.json</li>
  <li>HTTP Method: GET</li>
  <li>Content Type: json</li>
</ul>

<p>
  Sample response for https://hacker-news.firebaseio.com/v0/item/35908337.json:
</p>
<pre>
    <code>
    {`{
        by: "jamilbk",
        score: 1,
        time: 1683838872,
        title: "Firezone (YC W22) is hiring Elixir and Rust engineers",
        type: "job",
        url: "https://www.ycombinator.com/companies/firezone/jobs",
    }`}
    </code>
</pre>

<h3>Getting started</h3>
<p>You can create your app in `src/routes/app/+page.svelte`</p>
<p>
  <a title="App page" target="_blank" rel="noopener noreferrer" href="/app"
    >App page</a
  >
</p>

<h3>Notes</h3>
<p>
  The focus of this question is on functionality and not on styling, but feel
  free to beautify the page.
</p>
<p>
  To improve the user experience and avoid overfetching, you may want to limit
  the number of job details fetched to the number of jobs visible on the page.
</p>

<h3>Ui example</h3>

<img width="550" alt="job posting" src="/job-board-example.png" />
