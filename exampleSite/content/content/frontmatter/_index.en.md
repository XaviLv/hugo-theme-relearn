+++
tags = ["reference"]
title = "Front Matter Reference"
weight = 6
+++

Each page in Hugo **has to define** front matter.

On top of [Hugo's front matter](https://gohugo.io/content-management/front-matter/#fields), you can use the additional theme settings listed below.

A front matter provided by the theme is marked with a {{% badge style="green" icon="fa-fw fab fa-markdown" title=" " %}}Front Matter{{% /badge %}} badge throughout the documentation.

You set each theme front matter directly in the root of your page's front matter. For example, setting `math`

{{< multiconfig fm=true >}}
  math = true
{{< /multiconfig >}}

## Index

{{% taxonomy "frontmatter" "h3" %}}

## All Front Matter

The example reflect example values. The defaults can be taken from the [annotated example](#annotated-front-matter) below or the individual documentation.

{{< multiconfig fm=true >}}
{{% include "frontmatter.toml" %}}
{{< /multiconfig >}}

## Annotated Front Matter

````toml {title="toml"}
+++
{{% include "frontmatter.toml" %}}+++
````

## Some Detailed Examples

### Add Icon to a Menu Entry

In the page front matter, add a `menuPre` param to insert any HTML code before the menu label. The example below uses the GitHub icon.

{{< multiconfig fm=true >}}
title = "GitHub repo"
menuPre = "<i class='fab fa-github'></i> "
{{< /multiconfig >}}

![Title with icon](frontmatter-icon.png?width=18.75rem)

### Ordering Sibling Menu/Page Entries

Hugo provides a [flexible way](https://gohugo.io/content/ordering/) to handle order for your pages.

The simplest way is to set `weight` parameter to a number.

{{< multiconfig fm=true >}}
title = "My page"
weight = 5
{{< /multiconfig >}}

### Using a Custom Title for Menu Entries

By default, the Relearn theme will use a page's `title` attribute for the menu item.

But a page's title has to be descriptive on its own while the menu is a hierarchy. Hugo adds the `linkTitle` parameter for that purpose:

For example (for a page named `content/install/linux.md`):

{{< multiconfig fm=true >}}
title = "Install on Linux"
linkTitle = "Linux"
{{< /multiconfig >}}

### Override Expand State Rules for Menu Entries

You can change how the theme expands menu entries on the side of the content with the `alwaysopen` setting on a per page basis. If `alwaysopen=false` for any given entry, its children will not be shown in the menu as long as it is not necessary for the sake of navigation.

The theme generates the menu based on the following rules:

- all parent entries of the active page including their siblings are shown regardless of any settings
- immediate children entries of the active page are shown regardless of any settings
- if not overridden, all other first level entries behave like they would have been given `alwaysopen=false`
- if not overridden, all other entries of levels besides the first behave like they would have been given `alwaysopen=true`
- all visible entries show their immediate children entries if `alwaysopen=true`; this proceeds recursively
- all remaining entries are not shown

You can see this feature in action on the example page for [children shortcode](shortcodes/children) and its children pages.

## Disable Section Pages

You may want to structure your pages in a hierarchical way but don't want to generate pages for those sections? The theme got you covered.

To stay with the initial example: Suppose you want `level-one` appear in the sidebar but don't want to generate a page for it. So the entry in the sidebar should not be clickable but should show an expander.

For this, open `content/level-one/_index.md` and add the following front matter

{{< multiconfig fm=true >}}
collapsibleMenu = true
[_build]
  render = "never"
{{< /multiconfig >}}