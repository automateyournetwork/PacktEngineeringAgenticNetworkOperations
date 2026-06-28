# Spec — Packet Quest: a network routing adventure

## What I want to build
A web-based game where the player is a network packet trying to reach its destination. The player is shown a network topology and must make routing decisions at each hop — choosing the correct next-hop router based on routing tables, subnet masks, and protocol rules. If they choose wrong, the packet is "dropped" and the game explains exactly why that path fails. Success means the packet reaches its destination with full understanding of how it got there.

## Why this exists
Network routing is conceptually simple but notoriously hard to internalize. Reading about it doesn't build the routing intuition that engineers need. Walking *through* the process as a packet — hop by hop, decision by decision — creates the muscle memory that textbooks can't.

## Core learning outcomes
By completing the game, a player should be able to:
- Read an IPv4 routing table and identify the correct next hop
- Explain why a packet takes one path over another (longest prefix match, metric)
- Understand what happens when no route exists (ICMP unreachable)
- Identify common misconfigurations that cause routing loops or black holes
- Explain the difference between static routes and dynamic routing protocol entries

## Gameplay loop
1. Player is shown a simplified network topology (5–8 routers, labeled interfaces)
2. Player is shown the packet's source, destination, and a routing table for the current router
3. Player selects the next hop by clicking an interface or router
4. Game validates the choice against the actual routing table logic
5. Correct: packet moves, brief explanation of why this hop was right
6. Incorrect: packet dropped, detailed explanation of the mistake, option to retry
7. After delivery: summary of the path taken, full explanation of each decision

## Content scope (version 1)
- 8 levels, each introducing one new concept: default route, host route, subnet masking, longest prefix match, ECMP (equal-cost multipath), static vs. dynamic, TTL expiry, ICMP unreachables
- Each level has a pre-level "briefing" that teaches the concept before testing it
- No time pressure in v1 — players can take as long as they need
- A "hint" system that reveals one layer of the routing decision at a time

## What the game explicitly does not do
- Does not simulate actual routing protocols running live (no OSPF convergence animation in v1)
- Does not teach switching, VLANs, or Layer 2 (separate game)
- Does not connect to external systems or require login
- Does not use AI to generate questions at runtime — all content is pre-authored and verified