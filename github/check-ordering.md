# Better ordering of PR checks
> ⚠️ This is actually built into Refined GitHub by default, you just need to enable the :has selector in firefox:
> Go to `about:settings` and enable `layout.css.has-selector.enabled`



Puts more relevant checks at the top of the list, so you don't have to look for them by scrolling:
![image](https://github.com/annervisser/knowledge-base/assets/5613416/882b02fd-0603-4671-806a-9f4afd21b32e)


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
