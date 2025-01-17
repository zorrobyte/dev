AVL Tree
===

Adelson-Velsky and Landis ([AVL](https://en.wikipedia.org/wiki/AVL_tree)).

AVL trees are surprisingly subtle when it comes to their update rules.
This is a short note on some of those subtleties when implementing
AVL trees.

AVL Condition
---

The AVL condition is to make sure the balance factor (BF) of every node
stays within $\{-1,0,1\}$.
That is, the height of every nodes children differs by at most 1.

For every insertion and deletion, the BF is restored through a series
of tree rotations.
Tree rotations restore the BF locally, recursively applying any
height changes up the tree, issuing tree rotations as necessary.

Tree Updates
---


Tree insertion and deletions are initially done as normal
for a binary tree with tree rotations done afterwards
to fix nodes that violate the AVL condition.
Addition is done through a binary search and node addition
as a leaf whereas deletion is done through a surgery operation
which will be described in more detail below.

Tree rotations, while conceptually simple, are a bit
subtle as the balance factor needs to be potentially updated
for each of the nodes in addition to communicating
how the height of the sub-tree has changed to the parent.

The following diagram can be used as a reference
for how insertion and deletions change a tree
and how nodes need to be updated in relation to the
rotations:

![AVL Tree Rotations](img/avl_rot1.svg)

Here, the `--`, `-`, `+`, `==` and $\rlap{0}/$ signify
whether the node is left heavy requiring a rotation, left
heavy without the need for a rotation,, right heavy without
the need for a rotation, right
heavy with the need for a rotation or balanced,
respectively.

Note that the $\oplus$ and $\ominus$ represent
the addition or deletion of a node respectively.

The first two rows represent a simple rotation whereas
the last row is often represented by two simple rotations.

The tree height before the insertion or deletion
can be seen on the appropriate nodes or sub-trees 
with the height followed by the $\oplus$ or $\ominus$
symbol.
The arrow pointing up from the sub-tree root node
indicates codes for the height change message passed
to the parent node.

For example, the configuration where $x$ is unbalanced
and left heavy ($--$) with $y$ balanced but left heavy ($-$)
would have been the result of an addition
of a node to the $\alpha$ sub-tree or a removal of
a node from the $\gamma$ sub-tree.
In this case, the sub-tree's height rooted at $x$
would have been $h+2$ before the addition or
$h+1$ before the deletion,
following from the sub-tree $\alpha$ being at
height $h-1$ or the sub-tree $\gamma$ being
at height $h$ respectively.
After the insertion or deletion, the sub-tree
rooted at $y'$ would be $h+1$, leaving the
total sub-tree height unchanged in the case
of an addition or being reduced by one, in
the case of a deletion.


The following tables can help understand the state
of each of the nodes' balance factor, messages
passed to the parent and the various heights of sub-trees:

#### Single Rotation


|   |   |   |   |   |
|---|---|---|---|---|
| $\Delta h _ {x}$          | $-2$  | $-2$  | $2$   | $2$   |
| $\Delta h _ {y}$          | $-1$  | $0$   | $1$   | $0$   |
| $\Delta h _ {x'}$         | $0$   | $-1$  | $0$   | $1$   |
| $\Delta h _ {y'}$         | $0$   | $1$   | $0$   | $-1$  |
| $h _ { x' }$              | $h$   | $h+1$ | $h$   | $h+1$ |
| $h _ { y' }$              | $h+1$ | $h+2$ | $h+1$ | $h+2$ |
| $\Delta h _ {p'} \oplus$  | $0$   | $1$   | $0$   | $1$   |
| $\Delta h _ {p'} \ominus$ | $-1$  | $0$   | $-1$  | $0$   |

#### Double Rotation

In the case of a double rotation, the rotated nodes' balance factor, $x'$, $y'$ and $z'$,
can be determined from the $z$'s balance factor before rotation:

| $\Delta h _ z$ | $-1$ | $\rlap{0}/$ | $1$ | $-1$ | $\rlap{0}/$ | $1$ |
|---|---|---|---|---|---|---|
| $\Delta h _ {x}$  | $-2$ | $-2$ | $-2$ | $2$ | $2$ | $2$ |
| $\Delta h _ {y}$  | $1$ | $1$ | $1$ | $-1$ | $-1$ | $-1$ |
| $h _ \beta$  | $h -1$ | $h -1$ | $h -2$ | $h -1$ | $h -1$ | $h -2$ |
| $h _ \gamma$ | $h -2$ | $h -1$ | $h -1$ | $h -2$ | $h -1$ | $h -1$ |
| $\Delta h _ {x'}$ | $1$ | $\rlap{0}/$ | $\rlap{0}/$ | $\rlap{0}/$ | $\rlap{0}/$ | $-1$ |
| $\Delta h _ {y'}$ | $\rlap{0}/$ | $\rlap{0}/$ | $-1$ | $1$ | $\rlap{0}/$ | $\rlap{0}/$ |
| $\Delta h _ {z'}$ | $\rlap{0}/$ | $\rlap{0}/$ | $\rlap{0}/$ | $\rlap{0}/$ | $\rlap{0}/$ | $\rlap{0}/$ |
| $\Delta h _ {p'} \oplus$ | $\rlap{0}/$ | $\rlap{0}/$ | $\rlap{0}/$ | $\rlap{0}/$ | $\rlap{0}/$ | $\rlap{0}/$ |
| $\Delta h _ {p'} \ominus$ | $-1$ | $-1$ | $-1$ | $-1$ | $-1$ | $-1$ |

For brevity, here is a restriction of the table to highlight the nodes we care about most:

| $\Delta h$ | $-1$ | $\rlap{0}/$ | $1$ | $-1$ | $\rlap{0}/$ | $1$ |
|---|---|---|---|---|---|---|
| $\Delta h _ {x'}$ | $1$ | $\rlap{0}/$ | $\rlap{0}/$ | $\rlap{0}/$ | $\rlap{0}/$ | $-1$ |
| $\Delta h _ {y'}$ | $\rlap{0}/$ | $\rlap{0}/$ | $-1$ | $1$ | $\rlap{0}/$ | $\rlap{0}/$ |
| $\Delta h _ {p'} \oplus$ | $\rlap{0}/$ | $\rlap{0}/$ | $\rlap{0}/$ | $\rlap{0}/$ | $\rlap{0}/$ | $\rlap{0}/$ |
| $\Delta h _ {p'} \ominus$ | $-1$ | $-1$ | $-1$ | $-1$ | $-1$ | $-1$ |

In the case of an addition, the sub-tree would have had height $h+1$ before
the addition, with the resulting
sub-tree after the addition remaining at height $h+1$, needing no height change to the parent.
In the case of an deletion, the sub-tree would have had height $h+2$ before the deletion,
with the resulting sub-tree being at height $h-1$, requiring a message passed to the parent
of the updated height change.

---

When doing rotations, care has to be taken to make sure the privileged root pointer is updated
if it's involved in any rotations.


Deletion
---

![avl deletion](img/avl_del.svg)

Deletion of the node $z$ has three main cases (as per [CLR](https://en.wikipedia.org/wiki/Introduction_to_Algorithms)):

* $z$ is a leaf, in which case the parents point to $z$ can be set to `null`
* $z$ has exactly one child, in which case $z$ can be removed and the parent
  can now point to the child of $z$
* $z$ has two children, in which case, $y$, the successor of $z$ is found,
  removed and replaced with $z$. $y$ must have a `null` child so the initial
  removal can be done as per above

The last case requires surgery, stitching $y$ into $x$'s position and fixing up
the pointers for the node $y$ was removed from in $\beta$ and $\gamma$.
Special care has to be taken should the successor of $x$ be $y$.
In this special case, $y$ will
have $x$ as its parent and be $x$'s right child.

For example, the following code will work:

```
dT=0;
y->dh = x->dh;
y = succ(x);

// fix up y's parent
//
p = y->p;
if (p) {
  dh = p->dh;

  if   (lchild(y))  { p->l = y->r; dT =  1; }
  else              { p->r = y->r; dT = -1; }

  if (y->r)         { y->r->p = p; }
}

// remove x from tree, putting y in its place
//
if (x->p) {
  if (lchild(x))  { x->p->l = y; }
  else            { x->p->r = y; }
}
y->p = x->p;
y->r = x->r;
y->l = x->l;

if (y->r) { y->r->p = y; }
if (y->l) { y->l->p = y; }

if (root == x) { root = y; }
if (p == x) { p = y; }
if (p) { p->dh = dh + dT; }

free(x);

retrace(p, dT);
```

Should the parent of $y$ initially be $x$, we not
not only need to keep a copy of $x$'s balance factor,
as it will be discarded when we remove $x$ from the tree,
but we need to explicitly account for it when updating
the original parent of $y$'s balance factor in the
last two lines of the above.

In the above, root is also updated appropriately.

The last line, `retrace` is described below.

#### Retrace

There are some basic statements about the state of the tree during the recursion:

* Should a parent node's balance factor be changed, this necessarily corresponds
  to a sub-tree height change that will be communicated to the retrace function.
  Without a height change, the parent node's balance factor wouldn't have been
  altered in the first place.
* Not immediately obvious but the height of the root node of the sub-tree after a rotation
  will only ever result in the same height before the insert or delete operation
  or be changed in the appropriate direction. The height change is non increasing
  in magnitude as it's shuttled up the tree.

This means that if we are in the `retrace` function and considering a
node whose balance factor is $\{-1,0,1\}$ without a height change
communication, we don't need to rotate the sub-tree and only
need to recursively go up, communicating the height change as necessary.
More specifically, if no height change is communicated and the node is
balanced, no height change needs to be communicated up the tree.
If the height change is negative and the balance factor is $0$, we
need to keep communicating the negative height change up.
If the height change is positive and the balance factor is $\{-1,1\}$,
we need to keep communicating the height change up the tree.

In the case of an unbalanced node, the sub-tree should be re-balanced
with the parent node's height changing with the height change communicated.


Once an addition has been carried out and a rotation has potentially
occurred, the parent nodes need to be updated recursively.
This step can be referred to as a `retrace` step.

Tree rotations will leave the considered sub-tree in a consistent
state but still might leave some parent nodes in an unbalanced state.
Just knowing the balance factor of a node when recursively updating
the tree from an insertion or deletion does is not enough information
to properly handle rebalancing, the relative sub-tree height change
also needs to be known.
That is, not only does the balance factor of the current node
need to be considered, the balance factor transition needs to
be considered to account for height changes.

The height change will only ever be at most one, limiting the
balance factor of each node up the recursion.

After rebalancing the current sub-tree, the balance factor of
the parent is adjusted before recurring.
The change of the height of the sub-tree indicates what communicated
height change is given to the parent.

When landing on a node during the recursion, it must have been
in a consistent state previous to balance factor alteration,
so it was one of $\{-1,0,1\}$.

| Transition        | $\Delta T = -1$ | $\Delta T = 1$ | Action |
|-------------------|-----------------|----------------|--------|
| $- \to \rlap{0}/$ | $-$             | $\rlap{0}/$    | retrace( parent, $-\delta( \Delta T + 1)$ ) |
| $+ \to \rlap{0}/$ | $-$             | $\rlap{0}/$    | retrace( parent, $-\delta( \Delta T + 1)$ ) |
| $\rlap{0}/ \to -$ | $\rlap{0}/$     | $+$            | retrace( parent, $\delta( \Delta T - 1)$ ) |
| $\rlap{0}/ \to +$ | $\rlap{0}/$     | $+$            | retrace( parent, $\delta( \Delta T - 1)$ ) |
| $+ \to ++$        | $\rlap{0}/$     | $+$            |
| $- \to --$        | $\rlap{0}/$     | $+$            |




###### 2024-02-13
