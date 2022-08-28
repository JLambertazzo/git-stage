<template>
  <vue-command :commands="commands" :prompt="prompt" title="git-stage" />
</template>

<script setup>
import VueCommand, { createStdout } from "vue-command";
import "vue-command/dist/vue-command.css";
import cond from "lodash/fp/cond";
import isEqual from "lodash/fp/isEqual";
import pipe from "lodash/fp/pipe";
import get from "lodash/fp/get";
import stubTrue from "lodash/fp/stubTrue";
import { computed, ref } from "vue";
import constant from "lodash/fp/constant";
import { compact } from "lodash";

const DEFAULT_BRANCH = "master";

const unknown_command = () => createStdout("Error: unknown command");
const subcommand_is = (target) => pipe(get(["_", 1]), isEqual(target));

const git_init = ({ b }) => {
  if (branch.value) {
    return createStdout(`Repository already exists.. try something else!`);
  }
  branch.value = b || DEFAULT_BRANCH;
  return createStdout(
    `Initialized git repository on branch ${b || DEFAULT_BRANCH}`
  );
};

const git_stage = ({ _, p }) => {
  if (!branch.value) {
  }
  const [, , ...filenames] = compact([..._, p || undefined]);
  return createStdout(`staging files ${JSON.stringify(filenames)}`);
};
const git_commit = (opts) => createStdout("git_commit in progress");
const git_push = (opts) => createStdout("git_push in progress");

const branch = ref("");

const git = (opts) => {
  return cond([
    [subcommand_is("init"), git_init],
    [subcommand_is("stage"), git_stage],
    [subcommand_is("commit"), git_commit],
    [subcommand_is("push"), git_push],
    [stubTrue, unknown_command],
  ])(opts);
};

const commands = {
  test: (opts) => createStdout(JSON.stringify(opts)),
  git,
};

const prompt = computed(
  constant(`$ user${branch.value ? "@" : ""}${branch.value}`)
);
</script>
