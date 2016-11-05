---
layout: section
order: 3
title: Navigating
---

### Jumping to definition

The default command is `:EnDeclaration`. Since you'll likely be using this pretty often it makes sense to remap it. Personally I use:

```
au FileType scala nnoremap <localleader>df :EnDeclaration<CR>
```

If you want to open the declaration in a new split instead of the current buffer use `:EnDeclarationSplit` instead. `:EnDeclarationSplit v` creates a vertical split.

### Open Documentation For Browsing

`:EnDocBrowse` opens documentation for the element under the cursor in your browser. You can [customize which browser is opened][custom browser].

For more information, use `:h ensime`.

[custom browser]: https://ensime.github.io/editors/vim/install/#post-install-config
