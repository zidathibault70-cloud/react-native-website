# On demande des informations à l'utilisateur
prenom = input("Quel est ton prénom ? ")
annee_naissance = input("En quelle année es-tu né(e) ? ")

# On calcule l'âge
age = 2026 - int(annee_naissance)

# On affiche le message
print(f"Enchanté {prenom} ! En 2026, tu as ou tu auras {age} ans.")
