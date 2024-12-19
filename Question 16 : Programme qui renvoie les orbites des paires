from sage.all import *
from math import sqrt, isclose
import itertools

# Fonction auxiliaire pour comparer deux vecteurs avec tolérance
def vectors_are_close(v1, v2, tol=1e-6):
    return all(isclose(a, b, abs_tol=tol) for a, b in zip(v1, v2))

# Fonction pour arrondir les coordonnées des vecteurs
def round_vector(v, decimals=6):
    return tuple(round(float(coord), decimals) for coord in v)

# Directions autorisées (axes principaux et diagonales du cube)
def is_valid_direction(v):
    valid_directions = [
        vector([1, 0, 1]), vector([1, 1, 0]), vector([1, -1/sqrt(2), -1/sqrt(2)]),
    vector([1, 1/sqrt(2), -1/sqrt(2)]), vector([1, -1/sqrt(2), 1/sqrt(2)]),
    vector([1, 1/sqrt(2), 1/sqrt(2)]), vector([1, -1/sqrt(2), 0]),
    vector([1, 1/sqrt(2), 0]), vector([1, 0, 0]), vector([1, 0, -1/sqrt(2)]),
    vector([1, 0, 1/sqrt(2)]), vector([-1, 0, 1]), vector([0, -1, 1]),
    vector([0, 1, 1]), vector([-1/sqrt(2), 0, 1]), vector([1/sqrt(2), 0, 1]),
    vector([0, 0, 1]), vector([0, -1/sqrt(2), 1]), vector([0, 1/sqrt(2), 1]),
    vector([-1/sqrt(2), -1/sqrt(2), 1]), vector([1/sqrt(2), -1/sqrt(2), 1]),
    vector([-1/sqrt(2), 1/sqrt(2), 1]), vector([1/sqrt(2), 1/sqrt(2), 1]),
    vector([-1, 1, 0]), vector([-1/sqrt(2), 1, 0]), vector([1/sqrt(2), 1, 0]),
    vector([0, 1, 0]), vector([-1/sqrt(2), 1, 1/sqrt(2)]),
    vector([-1/sqrt(2), 1, -1/sqrt(2)]), vector([1/sqrt(2), 1, 1/sqrt(2)]),
    vector([1/sqrt(2), 1, -1/sqrt(2)]), vector([0, 1, -1/sqrt(2)]),
    vector([0, 1, 1/sqrt(2)])
    ]
    return any(vectors_are_close(v, d) for d in valid_directions)

# Générer les rotations du cube
def generate_rotations():
    rot_x = matrix([[1, 0, 0], [0, 0, -1], [0, 1, 0]])
    rot_y = matrix([[0, 0, 1], [0, 1, 0], [-1, 0, 0]])
    rot_z = matrix([[0, -1, 0], [1, 0, 0], [0, 0, 1]])

    rotations_set = set()
    for i, j, k in itertools.product(range(4), repeat=3):
        R = rot_x**i * rot_y**j * rot_z**k
        rotations_set.add(tuple(map(tuple, R)))
    return [matrix(r) for r in rotations_set]

# Calcul des orbites
def calculate_pair_orbits(pairs, rotations):
    visited = set()
    orbites = []

    for pair in pairs:
        if tuple(pair) not in visited:
            orbit = set()
            for M in rotations:
                transformed_pair = tuple(sorted(round_vector(M * vector(v)) for v in pair))
                # Vérifier que les vecteurs sont dans des directions valides
                if all(is_valid_direction(v) for v in transformed_pair):
                    for other_pair in pairs:
                        other_sorted = tuple(sorted(round_vector(v) for v in other_pair))
                        if all(vectors_are_close(a, b) for a, b in zip(transformed_pair, other_sorted)):
                            orbit.add(tuple(other_pair))
                            visited.add(tuple(other_pair))
            if orbit:  # Ajouter uniquement les orbites non vides
                orbites.append(orbit)
    return orbites

# Étape principale
def main():
    pairs = [
        ((1, 0, 1), (-1, 0, 1)),
((1, 0, 1), (0, 1, 0)),
((1, 0, 1), (-1/2*sqrt(2), 1, 1/2*sqrt(2))),
((1, 0, 1), (1/2*sqrt(2), 1, -1/2*sqrt(2))),
((1, 1, 0), (0, 0, 1)),
((1, 1, 0), (1/2*sqrt(2), -1/2*sqrt(2), 1)),
((1, 1, 0), (-1/2*sqrt(2), 1/2*sqrt(2), 1)),
((1, 1, 0), (-1, 1, 0)),
((1, -1/2*sqrt(2), -1/2*sqrt(2)), (1, 1/2*sqrt(2), 1/2*sqrt(2))),
((1, -1/2*sqrt(2), -1/2*sqrt(2)), (0, -1, 1)),
((1, -1/2*sqrt(2), -1/2*sqrt(2)), (1/2*sqrt(2), 0, 1)),
((1, -1/2*sqrt(2), -1/2*sqrt(2)), (1/2*sqrt(2), 1, 0)),
((1, 1/2*sqrt(2), -1/2*sqrt(2)), (1, -1/2*sqrt(2), 1/2*sqrt(2))),
((1, 1/2*sqrt(2), -1/2*sqrt(2)), (0, 1, 1)),
((1, 1/2*sqrt(2), -1/2*sqrt(2)), (1/2*sqrt(2), 0, 1)),
((1, 1/2*sqrt(2), -1/2*sqrt(2)), (-1/2*sqrt(2), 1, 0)),
((1, -1/2*sqrt(2), 1/2*sqrt(2)), (0, 1, 1)),
((1, -1/2*sqrt(2), 1/2*sqrt(2)), (-1/2*sqrt(2), 0, 1)),
((1, -1/2*sqrt(2), 1/2*sqrt(2)), (1/2*sqrt(2), 1, 0)),
((1, 1/2*sqrt(2), 1/2*sqrt(2)), (0, -1, 1)),
((1, 1/2*sqrt(2), 1/2*sqrt(2)), (-1/2*sqrt(2), 0, 1)),
((1, 1/2*sqrt(2), 1/2*sqrt(2)), (-1/2*sqrt(2), 1, 0)),
((1, -1/2*sqrt(2), 0), (0, 0, 1)),
((1, -1/2*sqrt(2), 0), (1/2*sqrt(2), 1, 0)),
((1, -1/2*sqrt(2), 0), (1/2*sqrt(2), 1, 1/2*sqrt(2))),
((1, -1/2*sqrt(2), 0), (1/2*sqrt(2), 1, -1/2*sqrt(2))),
((1, 1/2*sqrt(2), 0), (0, 0, 1)),
((1, 1/2*sqrt(2), 0), (-1/2*sqrt(2), 1, 0)),
((1, 1/2*sqrt(2), 0), (-1/2*sqrt(2), 1, 1/2*sqrt(2))),
((1, 1/2*sqrt(2), 0), (-1/2*sqrt(2), 1, -1/2*sqrt(2))),
((1, 0, 0), (0, -1, 1)),
((1, 0, 0), (0, 1, 1)),
((1, 0, 0), (0, 0, 1)),
((1, 0, 0), (0, -1/2*sqrt(2), 1)),
((1, 0, 0), (0, 1/2*sqrt(2), 1)),
((1, 0, 0), (0, 1, 0)),
((1, 0, 0), (0, 1, -1/2*sqrt(2))),
((1, 0, 0), (0, 1, 1/2*sqrt(2))),
((1, 0, -1/2*sqrt(2)), (1/2*sqrt(2), 0, 1)),
((1, 0, -1/2*sqrt(2)), (1/2*sqrt(2), -1/2*sqrt(2), 1)),
((1, 0, -1/2*sqrt(2)), (1/2*sqrt(2), 1/2*sqrt(2), 1)),
((1, 0, -1/2*sqrt(2)), (0, 1, 0)),
((1, 0, 1/2*sqrt(2)), (-1/2*sqrt(2), 0, 1)),
((1, 0, 1/2*sqrt(2)), (-1/2*sqrt(2), -1/2*sqrt(2), 1)),
((1, 0, 1/2*sqrt(2)), (-1/2*sqrt(2), 1/2*sqrt(2), 1)),
((1, 0, 1/2*sqrt(2)), (0, 1, 0)),
((-1, 0, 1), (0, 1, 0)),
((-1, 0, 1), (-1/2*sqrt(2), 1, -1/2*sqrt(2))),
((-1, 0, 1), (1/2*sqrt(2), 1, 1/2*sqrt(2))),
((0, -1, 1), (0, 1, 1)),
((-1/2*sqrt(2), 0, 1), (0, 1, 0)),
((1/2*sqrt(2), 0, 1), (0, 1, 0)),
((0, 0, 1), (-1, 1, 0)),
((0, 0, 1), (-1/2*sqrt(2), 1, 0)),
((0, 0, 1), (1/2*sqrt(2), 1, 0)),
((0, 0, 1), (0, 1, 0)),
((0, -1/2*sqrt(2), 1), (-1/2*sqrt(2), 1, 1/2*sqrt(2))),
((0, -1/2*sqrt(2), 1), (1/2*sqrt(2), 1, 1/2*sqrt(2))),
((0, -1/2*sqrt(2), 1), (0, 1, 1/2*sqrt(2))),
((0, 1/2*sqrt(2), 1), (-1/2*sqrt(2), 1, -1/2*sqrt(2))),
((0, 1/2*sqrt(2), 1), (1/2*sqrt(2), 1, -1/2*sqrt(2))),
((0, 1/2*sqrt(2), 1), (0, 1, -1/2*sqrt(2))),
((-1/2*sqrt(2), -1/2*sqrt(2), 1), (1/2*sqrt(2), 1/2*sqrt(2), 1)),
((-1/2*sqrt(2), -1/2*sqrt(2), 1), (-1, 1, 0)),
((-1/2*sqrt(2), -1/2*sqrt(2), 1), (0, 1, 1/2*sqrt(2))),
((1/2*sqrt(2), -1/2*sqrt(2), 1), (-1/2*sqrt(2), 1/2*sqrt(2), 1)),
((1/2*sqrt(2), -1/2*sqrt(2), 1), (0, 1, 1/2*sqrt(2))),
((-1/2*sqrt(2), 1/2*sqrt(2), 1), (0, 1, -1/2*sqrt(2))),
((1/2*sqrt(2), 1/2*sqrt(2), 1), (-1, 1, 0)),
((1/2*sqrt(2), 1/2*sqrt(2), 1), (0, 1, -1/2*sqrt(2))),
((-1/2*sqrt(2), 1, 1/2*sqrt(2)), (1/2*sqrt(2), 1, -1/2*sqrt(2))),
((-1/2*sqrt(2), 1, -1/2*sqrt(2)), (1/2*sqrt(2), 1, 1/2*sqrt(2))),
    ]

    # Générer les rotations
    rotations = generate_rotations()

    # Calculer les orbites
    orbites = calculate_pair_orbits(pairs, rotations)

    # Afficher les résultats
    print(f"Nombre d'orbites trouvées : {len(orbites)}")
    for i, orbit in enumerate(orbites, 1):
        print(f"Orbite {i}: {orbit}")

if __name__ == "__main__":
    main()
