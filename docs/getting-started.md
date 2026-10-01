def traiter_depot(user, montant_depose_xof):
    """
    Gestion des dépôts en Francs CFA (XOF)
    """
    # 1. CAS DÉVELOPPEUR : Pas de frais, pas de pièce d'identité
    if user.is_developer:
        commission = 0
        montant_credite = montant_depose_xof
        print(f"[DEV] Recharge de {montant_credite} XOF effectuée sans aucun frais.")

    # 2. CAS UTILISATEUR STANDARD : Application des frais (ex: 10%)
    else:
        if not user.piece_identite_validee:
            raise ValueError("Veuillez fournir votre pièce d'identité avant de recharger.")
            
        taux_commission = 0.10  # 10 %
        commission = montant_depose_xof * taux_commission
        montant_credite = montant_depose_xof - commission
        
        print(f"[CLIENT] Dépôt: {montant_depose_xof} XOF | Frais retenus: {commission} XOF | Crédité: {montant_credite} XOF")

    # Mise à jour du solde dans votre base de données
    user.solde_xof += montant_credite
    
    # Enregistrement de votre bénéfice dans votre compte admin
    garder_commission_admin(commission)

    return montant_credite
