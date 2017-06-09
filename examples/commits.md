# Examples of great commits from existing City of Austin projects

Below are commits that follow the Deliberate Git best practices around _what_ and _why_ they were created. They have been replicated here because some are from private repositories which viewers of this file might not have access to.

The format is:

> **[Commit title linking to commit in `master` branch]()**

> Commit message
>
> …
>
> …

> Commit author & date

### Austin Convention Center Website

> **[Work around IE bug impacting inline SVG height](47d7aa7506e0ff6d55269062012725e0af35482b)**

> By default, IE 10 and 11 render the interactive floor plan SVGs as only ~150px tall, regardless of their width. Additional CSS declarations don't seem to have any effect, so I resorted to setting the height manually, via JS, based on the SVG's viewBox aspect ratio.
>
> Note that the manual height doesn't update when the window is resized, but I don't think that's worth the trouble.

> [Jacob Paul](https://github.com/jcbpl) committed on Jan 2

### CitySpace

> **[Improve flexbox implementation](https://github.com/cityofaustin/cityspace/commit/c36e916e798593a255ae7a077ee2c90cf12bdb82)**

> `justify-content: space-between` makes the last item in a row float to the right when there are fewer items than columns. The`batch` tag in twig allows us to insert missing elements into arrays of a given size. While adding ‘blank’ items could be considered polluting the DOM for the sake of styling, I don’t think it’s terribly offensive.
>
> Had the block implementation been coded to account for the necessary margins between elements differently, we wouldn’t need to insert a spacer element, but it’s important to note that flex box is not a grid system in itself, and this is being used outside of any other grid system.
>
> To change from 3 to 2 or 4 columns across, update lines 57 and 58: `cityspace-flexbox-thirds` >> …`-halves` or …`-fourths` and `items|batch(3,` >> `items|batch(2` or `items|batch(4`.
>
> This update also allows for vertical centering of items in tiles.
>
> Tested back to IE10, where blocks line up in a single column as a fallback.
>
> Sources:
> https://stackoverflow.com/questions/18744164/flex-box-align-last-row-to-grid
> https://twig.sensiolabs.org/doc/2.x/filters/batch.html

> [Sarah Rudder](https://github.com/sknep) committed on May 30