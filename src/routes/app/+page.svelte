<script async script lang="ts">
  // Jobs list
  const apiListUrl = "https://hacker-news.firebaseio.com/v0/jobstories.json";

  // Job details
  const apiDetailsUrl = (id: number) =>
    `https://hacker-news.firebaseio.com/v0/item/${id}.json`;

  const PAGE_SIZE = 10;
  let isLoading = true;
  let currPage = 1;
  let jobs: any[] = [];
  let jobsList: any[] = [];

  async function fetchJobIds() {
    jobsList = await fetch(apiListUrl).then((x) => x.json());

    const start = currPage * PAGE_SIZE;
    const end = start + PAGE_SIZE;
    return jobsList.slice(start, end);
  }

  async function fetchJob() {
    const jobIdsForPage = await fetchJobIds();

    isLoading = true;
    const jobsForPage = await Promise.all(
      jobIdsForPage.map((jobId) =>
        fetch(apiDetailsUrl(jobId)).then((res) => res.json())
      )
    );
    jobs = [...jobs, ...jobsForPage];

    isLoading = false;
  }

  $: if (currPage) {
    fetchJob();
  }

  function loadMore() {
    currPage = currPage + 1;
  }
</script>

<div>
  {#each jobs as job}
    <div class="job">
      <h4 style="margin: 0;">
        <a target="_blank" rel="noopener noreferrer" href={job.url}>{job.url}</a
        >
      </h4>
      <p style="margin: 0">posted on: {new Date(job.time * 1000)}</p>
      <p style="margin: 0">by: {job.by}</p>
    </div>
  {/each}
  {#if isLoading}
    <p>Loading</p>
  {:else if jobs.length > 0 && currPage * PAGE_SIZE + PAGE_SIZE < jobsList.length}
    <button on:click={loadMore}> Load more </button>
  {/if}
</div>

<style>
  .job {
    padding: 20px;
    border: 1px solid silver;
    margin: 10px 0;
  }
</style>
