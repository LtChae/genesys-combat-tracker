<template>
  <div class="wrapper">
    <div class="identity-wrapper">
      <div class="stat-row">
        <input v-model="name" class="input-wide" placeholder="unnamed goon" />
      </div>
      <div class="stat-row">
        <div>
          <input type="radio" id="minion" value="minion" v-model="type" />
          <label for="minion">
            <img class="icon" src="../assets/backup.png" />
          </label>
        </div>
        <div>
          <input type="radio" id="rival" value="rival" v-model="type" />
          <label for="rival">
            <img class="icon" src="../assets/person.png" />
          </label>
        </div>
        <div>
          <input type="radio" id="nemesis" value="nemesis" v-model="type" />
          <label for="nemesis">
            <img class="icon" src="../assets/strong.png" />
          </label>
        </div>
      </div>
    </div>
    <div class="stats-wrapper">
      <div class="stat-row">
        <img class="icon" src="../assets/breastplate.png" />
        <input v-model="soak" class="input-small" />
        <img class="icon" src="../assets/swords-emblem.png" />
        <input v-model="meleeDefense" class="input-small" />
        <img class="icon" src="../assets/arrows-shield.png" />
        <input v-model="rangedDefense" class="input-small" />
      </div>
      <div class="stat-row" v-if="type == 'minion'">
        <div>
        <img class="icon" src="../assets/backup.png" />
        <input v-model="quantity" class="input-small" />
        </div>
        <div>
          <img class="icon" src="../assets/health-per-minion.png" />
          <input v-model="woundThreshold" class="input-small" />
        </div>
      </div>
      <div class="stat-row">
        <div>
          <img class="icon" src="../assets/heart-drop.png" />
          <input v-model="wounds" class="input-small" />
          <span>/</span>
          <input v-model="woundThreshold" class="input-small" v-if="type != 'minion'"/>
          <input v-model="minionThreshold" class="input-small" v-if="type == 'minion'" disabled/>
        </div>
      </div>
      <div class="stat-row" v-if="type == 'nemesis'">
        <div>
          <img class="icon" src="../assets/beams-aura.png" />
          <input v-model="strain" class="input-small" />
          <span>/</span>
          <input v-model="strainThreshold" class="input-small" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Entity",
  props: {},
  data: () => {
    return {
      name: "",
      soak: 0,
      wounds: 0,
      woundThreshold: 0,
      strain: 0,
      strainThreshold: 0,
      type: "nemesis",
      quantity: 0,
      meleeDefense: 0,
      rangedDefense: 0
    };
  },
  computed: {
    minionThreshold: function () {
      return this.quantity * this.woundThreshold
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.input-wide {
  width: 90%;
}
.input-small {
  width: 1.5rem;
}
.stat-row {
  width: 100%;
  display: flex;
  justify-content: space-between;
}
.icon {
  height: 1rem;
  vertical-align: middle;
}
.stats-wrapper {
  display: inline-flex;
  flex-wrap: wrap;
  justify-content: space-between;

  border: 1px solid black;
  padding: 5px;
}

.wrapper {
  width: 10rem;
}

.identity-wrapper {
  display: inline-flex;
  flex-wrap: wrap;
  justify-content: space-between;
}
</style>
