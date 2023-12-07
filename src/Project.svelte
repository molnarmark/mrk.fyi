<script>
  export let name;
  export let description;
  export let url;
  export let stars;
</script>

<div class="project">
    <h3 class="project-title"><a href="{url}">{name}</a></h3>
    <p class="project-description">{description}</p>
    <span class="project-stars">⭐ {stars}</span>
</div>

<style>
  .project {
    display: flex;
/*    flex: 1 0 30%;*/
    align-items: center;
    flex-direction: column;
    margin: 15px;
    background: #2072e008;
    border: solid 2px #2072e0;
    border-radius: 5px;
    position: relative;
    -webkit-box-shadow: 0px 5px 0px 0px #2072e050;
    -moz-box-shadow: 0px 5px 0px 0px #2072e050;
    box-shadow: 0px 5px 0px 0px #2072e050;
    transition: all 200ms ease-in-out;
    animation: fadeIn 2s;
    -webkit-animation: fadeIn 2s;
    -moz-animation: fadeIn 2s;
    -o-animation: fadeIn 2s;
    -ms-animation: fadeIn 2s;
  }

  .project:hover {
    cursor: pointer;
    background: linear-gradient(180deg, rgba(255, 0, 0, 0) 0%, rgba(12, 87, 189, 0.2) 67%);

  }

  .project-title {
    margin: 0;
    margin-top: 10px;
    font-size: 28px;
    text-align: center;
  }

  .project-title a {
    color: white;
  }

  .project-description {
    padding: 10px;
    font-size: 20px;
    text-align: center;
    margin-bottom: 40px;
  }

  .project-stars {
    position: absolute;
    bottom: 0;
    font-size: 22px;
  }
</style>
