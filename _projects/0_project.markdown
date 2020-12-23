---
layout: page
title: Economic Resource Availability
description: Analysis of a community's ability to whether financial setbacks through social lending.
img:
category:
importance: 1
---

*This project was completed as part of CS302 at UVM with Tom Nececkas and Mark Kirby. The following article is an overview of the project.*

The Fed published a [report](https://www.federalreserve.gov/publications/2019-economic-well-being-of-us-households-in-2018-preface.htm) where 40% of americans would have difficulty covering a $400 expense. Of those americans, 10% would borrow from a friend or family member to cover the expense. With an increasing number of people turning to crowdfunding sites such as [GoFundMe](https://gofundme.com) <sup>[1](https://www.cmaj.ca/content/184/2/E123.short)</sup>, it is clear that people are becoming more reliant on the community to provide finanical relief. Our work develops a potential model for networks resources to insulate people in a community from financial setbacks.

## Data

We used in income distribution from the Milwaukee Area Renters Study (MARS) which is publicly available [here](https://doi.org/10.7910/DVN/BLUU3U). The mean income is $1315.10 and median income is $1085.00. Approximately 13% report no income.

## Details

We developed a model consisting of the following parameters:

- $$n$$ nodes
- $$s$$ proportion of savings
- $$a$$ proportion of income that could be borrowed
- $$c$$ expense
- $$I_k$$ income of the *k*th individual

The goal was to determine the following using the MARS income distribution:

1. Determine the relationship between the reduction of financial resources in a community and the number of connections for the community to become financially stable.
2. Determine the relationship between each of the parameters and the number of connections.

A notion of "financial stability" is needed to find the relationships. An individual is considered financially stable if their expense $$c$$ can be covered with their own resources *or* in addition to the resources of a close neighbor. Formally,

$$ sI_k + \sum_{n\in\mathcal{N}_k}aI_n \ge c $$

where $$\mathcal{N}_k$$ is the neighborhood of the *k*th individual.

### Assumptions

1. Only an individual's income is considered.
2. Individuals can allocate resources to cover expenses.
3. Homogeneity. Everyone experiences the same financial setback and willingness to lend their resources.

In addition, the edges are created randomly. In reality, social networks are often structured.

### Procedure

Starting with $$n$$ disjoint nodes, we randomly create edges until the condition for financial stability is met following a relative reduction in the total income $$p\in\{0.05i \mid 0 \le i \le 20\}$$ and changing the parameters $$n\in\{20, 50, 100\}$$, $$s\in\{0.1, 0.2, 0.4\}$$, $$a\in\{0.1,0.2,0.4\}$$, and $$c\in\{400, 800, 1600\}$$. This is repeated for $$T=100$$ trials.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        <img class="rounded z-depth-1" src="{{ '/assets/img/era/procedure.svg' | relative_url }}">
    </div>
</div>
<div class="long caption">
    The process for analyzing the financial stability of nodes in a network with parameters of 20% savings and 10% access to neighbors’ resources according to the rules described above. The amount in parentheses is the node's savings. I) The initial proportion of nodes that are able to weather a $400 setback (blue) and those that are not (red). II) All resources are reduced by 25% and leaves only node 4 stable. III.a) If a random edge is added between nodes 1 and 2, both nodes become financially stable since each node's savings and the sum of the access to neighbors income is above the financial setback (the stabilizing condition.) III.b) If a random edge is added between nodes 3 and 4, the proportion of financially stable nodes do not change since node 3 fails to meet the stabilizing condition.
</div>

## Results

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        <img class="w-100 rounded z-depth-1" src="{{ '/assets/img/era/default.png' | relative_url }}">
    </div>
</div>
<div class="long caption">
    Number of edges for financial stability in the community with parameters n = 20, s = 0.2, a = 0.1, c = 400 (the default parameters). The solid black line is the total possible number of edges and the dashed black line is the average number of edges.
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        <img class="w-100 rounded z-depth-1" src="{{ '/assets/img/era/n-edge-scaling.png' | relative_url }}">
    </div>
</div>
<div class="caption">
    Number of edges for stability with respect to the expense (cost) grouped by the reduction in income.
</div>

The trend between expense and number of edges is almost linear until it approaches the maximum possible number of edges. However, the scaling from each reduction in income is non-linearly increasing. It indicates the the growth in the number of edges per percentrage reduction in income exceeds linear growth.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        <img class="w-100 rounded z-depth-1" src="{{ '/assets/img/era/n-node-edge-scaling.png' | relative_url }}">
    </div>
</div>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        <img class="w-100 rounded z-depth-1" src="{{ '/assets/img/era/prop-unstable-n-node.png' | relative_url }}">
    </div>
</div>
<div class="caption">
    (top) Number of edges for stability and (bottom) initial proportion of financially unstable nodes with parameters (left to right) <span class='d-inline-block'><i>n</i> = 20</span>, <span class='d-inline-block'><i>n</i> = 50</span>, and <span class='d-inline-block'><i>n</i> = 100.</span>
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        <img class="w-100 rounded z-depth-1" src="{{ '/assets/img/era/savings-edge-scaling.png' | relative_url }}">
    </div>
</div>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        <img class="w-100 rounded z-depth-1" src="{{ '/assets/img/era/prop-unstable-savings.png' | relative_url }}">
    </div>
</div>
<div class="caption">
    (top) Number of edges for stability and (bottom) initial proportion of financially unstable nodes with parameters (left to right) <span class='d-inline-block'><i>s</i> = 0.1</span>, <span class='d-inline-block'><i>s</i> = 0.2</span>, and <span class='d-inline-block'><i>s</i> = 0.4.</span>
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        <img class="w-100 rounded z-depth-1" src="{{ '/assets/img/era/cost-edge-scaling.png' | relative_url }}">
    </div>
</div>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        <img class="w-100 rounded z-depth-1" src="{{ '/assets/img/era/prop-unstable-cost.png' | relative_url }}">
    </div>
</div>
<div class="caption">
    (top) Number of edges for stability and (bottom) initial proportion of financially unstable nodes with parameters (left to right) <span class='d-inline-block'><i>c</i> = 400</span>, <span class='d-inline-block'><i>c</i> = 800</span>, and <span class='d-inline-block'><i>c</i> = 1600.</span>
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        <img class="w-100 rounded z-depth-1" src="{{ '/assets/img/era/access-edge-scaling.png' | relative_url }}">
    </div>
</div>
<div class="caption">
    (top) Number of edges for stability and (bottom) initial proportion of financially unstable nodes with parameters (left to right) <span class='d-inline-block'><i>a</i> = 0.1</span>, <span class='d-inline-block'><i>a</i> = 0.2</span>, and <span class='d-inline-block'><i>a</i> = 0.4.</span>
</div>

The trend between the number of edges with the number of people $$n$$ in the community, increasing access $$a$$ to resources, and expense $$c$$ is as expected:
1. More people in the network reduces the growth in the number of social connections to become financially stable.
2. Fewer social connections are needed for individuals to become financially stable with greater community resources.
3. Increasing costs increases the number of social connections.
The common idea for 1 and 2 is increased community resources which reduces the growth in the number of edges. On the other hand, increasing costs is analogous to reducing the resources available in the community.

For savings, the results were unexpected. While increased savings reduced the initial proportion of those financially unstable, the number of social connections does not change significantly. It might be the case that those that require the most number of social connections are those with significantly low income.
