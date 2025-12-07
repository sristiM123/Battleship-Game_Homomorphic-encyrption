# Battleship-Game_Homomorphic-encyrption
This project extends the traditional Battleship rules to a two-player, turn-based system in which both boards are stored and processed in encrypted form. All hit/miss evaluations are carried out homomorphically using Pyfhel’s BFV integer scheme.

A privacy-preserving implementation of the classic Battleship game using the BFV homomorphic encryption scheme (Pyfhel).
Each player’s board remains encrypted throughout the game; only the outcome of a shot (hit or miss) is revealed. This project demonstrates how encrypted computation can be applied to multi-party interactive applications without exposing private state.

# Key properties:
10×10 board for each player
Ships of sizes 5, 4, 3, 2, 2 placed randomly
Both boards are encrypted cell-by-cell
The program never accesses the plaintext board of the opponent
Hit detection is performed by homomorphic multiplication and selective decryption of a single ciphertext
The winner is the first player to destroy all opponent ships
This implementation is suitable for coursework, demonstrations of secure computation, or experimentation with applied homomorphic encryption.

# Technical Design
# Encryption Model

Each board cell is encoded as an integer:
0 = empty
1 = ship

The values are encrypted using BFV. A move consists of:
Attacker selects a coordinate.
Program retrieves the encrypted cell Enc(board[r][c]).
It multiplies by an encrypted constant Enc(1).
The result is decrypted to reveal only {0, 1}.
No structural information, positions of remaining ships, or neighbouring cells are ever revealed.

# Isolation of State
Each player maintains:
A plaintext board (for their own reference)
An encrypted board used for all computation by the opponent

Only local hits/misses are ever shown. Opponents never view each other’s ship placements.
