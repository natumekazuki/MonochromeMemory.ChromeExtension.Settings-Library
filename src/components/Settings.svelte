<script>
  import { onMount } from "svelte";
  import { getSettings, saveSettings } from "../utils/storage.js";

  export let configUrl = "../settings.json"; // デフォルトの設定ファイルの相対パス
  let config = []; // 設定項目の定義
  let settings = {}; // 現在の設定値

  // 設定のロード
  onMount(async () => {
    try {
      const response = await fetch(configUrl);
      config = await response.json();
    } catch (error) {
      console.error("設定ファイルをロードできませんでした:", error);
      return;
    }

    // ストレージから設定をロードし、デフォルト値を適用
    const storedSettings = await getSettings(config.map(c => c.key));
    config.forEach(item => {
      if (!(item.key in storedSettings)) {
        storedSettings[item.key] = item.default;
      }
    });

    // 初期値をストレージに保存
    await saveSettings(storedSettings);
    settings = storedSettings;
  });

  const updateSetting = async (key, value) => {
    settings[key] = value;
    await saveSettings({ [key]: value });
  };

  export const fetchSettings = () => {
    return settings;
  };
</script>

<div class="settings">
  {#if config.length > 0}
    {#each config as item}
      <div class="setting-item">
        <label>{item.label}</label>
        {#if item.type === "toggle"}
          <input
            type="checkbox"
            bind:checked={settings[item.key]}
            on:change={() => updateSetting(item.key, settings[item.key])}
          />
        {:else if item.type === "select"}
          <select
            bind:value={settings[item.key]}
            on:change={() => updateSetting(item.key, settings[item.key])}
          >
            {#each item.options as option}
              <option value={option}>{option}</option>
            {/each}
          </select>
        {:else if item.type === "text"}
          <input
            type="text"
            bind:value={settings[item.key]}
            on:input={() => updateSetting(item.key, settings[item.key])}
          />
        {/if}
      </div>
    {/each}
  {:else}
    <p>設定をロード中...</p>
  {/if}
</div>

<style>
  .settings {
    padding: 1em;
  }
  .setting-item {
    margin-bottom: 1em;
  }
  label {
    display: block;
    margin-bottom: 0.5em;
  }
</style>
