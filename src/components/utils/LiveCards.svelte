<script lang="ts">
  import {
    broadcasts,
    following,
    mayLike,
  } from '../../services/broadcasts';

  export let selected: boolean = true;
</script>

<style lang="scss">
  .lives {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-wrap: wrap;

    figure {
      min-width: 300px;
      margin: 1rem;
      position: relative;
      border-radius: 20px;
      cursor: pointer;

      span {
        position: absolute;
        display: flex;
        top: 60px;
        .live {
          display: flex;
          align-items: center;
          font-size: 1.5rem;
          padding: 0 1rem;
          border-top-left-radius: 10px;
          border-bottom-left-radius: 10px;
        }

        .views {
          left: 86px;
          display: flex;
          align-items: center;
          background-color: #353030;
          font-size: 1.5rem;
          padding: 0 1rem;
          border-top-right-radius: 10px;
          border-bottom-right-radius: 10px;
        }
      }

      img {
        min-width: 300px;
        object-fit: cover;
        border-radius: 20px;
      }

      p {
        position: absolute;
        color: white;
        bottom: 15px;
        left: 15px;
        margin: 0;
        font-size: 3rem;
        text-shadow: 2px 2px 2px black;
        z-index: 1;
        i {
          margin-right: 0.7rem;
        }
      }

      &::after {
        content: '';
        width: 100%;
        height: 20%;
        position: absolute;
        bottom: 6px;
        left: 0;
        background: linear-gradient(
          to top,
          black,
          rgba(black, 0)
        );
        opacity: 0.7;
        border-bottom-left-radius: 20px;
        border-bottom-right-radius: 20px;
      }
    }
  }
  .may-like {
    text-align: center;
    p {
      font-size: 1.7rem;
    }
  }
  .bg-blue {
    background-color: #2b63c8;
  }

  .bg-red {
    background-color: #d2202d;
  }
</style>

{#if selected}
  <div class="lives">
    {#each broadcasts as live}
      <figure>
        <span>
          <p class="live bg-blue">
            <i class="fas fa-video" />LIVE
          </p>
          <p class="views">
            <i class="fas fa-eye" />{live.views}
          </p>
        </span>
        <img src={live.img} alt="" />
        <p>{live.user}</p>
      </figure>
    {/each}
  </div>
{:else}
  <div class="lives">
    {#each following as follow}
      <figure>
        <span>
          <p class="live bg-red">
            <i class="fas fa-video" />LIVE
          </p>
          <p class="views">
            <i class="fas fa-eye" />{follow.views}
          </p>
        </span>
        <img src={follow.img} alt="" />
        <p>{follow.user}</p>
      </figure>
    {/each}
  </div>
  <div class="may-like">
    <p>You May Like:</p>
  </div>
  <div class="lives">
    {#each mayLike as like}
      <figure>
        <span>
          <p class="live bg-red">
            <i class="fas fa-video" />LIVE
          </p>
          <p class="views">
            <i class="fas fa-eye" />{like.views}
          </p>
        </span>
        <img src={like.img} alt="" />
        <p>{like.user}</p>
      </figure>
    {/each}
  </div>
{/if}
