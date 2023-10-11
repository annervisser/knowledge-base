# Better ordering of PR checks
Add this custom css to [Refined GitHub](https://github.com/refined-github/refined-github) or any custom stylesheet add-on:

```css
/** Show successful checks after other checks */
.merge-status-item:has(.octicon-check) {
  order: 1;
}

/** Show skipped checks after all other checks */
.merge-status-item:has(.octicon-skip) {
  order: 2;
}
```

<details>
  <summary>Refined Github Settings</summary>

  ![image](https://github.com/annervisser/knowledge-base/assets/5613416/29c7c1bc-9098-4491-a490-157d8a02c165)
</details>
