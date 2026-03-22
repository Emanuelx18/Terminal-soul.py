import random

def generate_damage(min_dmg, max_dmg):
    return random.randint(min_dmg, max_dmg)

def health_bar(hp, max_hp=100, length=10):
    filled = int((hp / max_hp) * length)
    return "[" + "#" * filled + "-" * (length - filled) + "]"

def show_status(hero_name, hero_hp, enemy_name, enemy_hp):
    print("\n--- CURRENT STATUS ---")
    print(f"{hero_name}: {hero_hp} HP {health_bar(hero_hp)}")
    print(f"{enemy_name}: {enemy_hp} HP {health_bar(enemy_hp, 120)}")
    print("----------------------\n")

def apply_critical(damage):
    if random.random() < 0.10:
        print(" Critical hit!")
        return damage * 2
    return damage

def player_turn(hero_hp, enemy_hp, potions):
    print("Choose your action:")
    print("1. Attack")
    print("2. Heal")
    print("3. Special Ability")

    choice = input("Enter option: ")

    if choice == "1":
        damage = generate_damage(10, 25)
        damage = apply_critical(damage)
        enemy_hp -= damage
        print(f"You attack and deal {damage} damage!")

    elif choice == "2":
        if potions > 0:
            hero_hp += 20
            potions -= 1
            print("You healed 20 HP!")
        else:
            print("No potions left! Choose another action.")
            return player_turn(hero_hp, enemy_hp, potions)

    elif choice == "3":
        if random.random() < 0.5:
            print(" Special attack failed!")
        else:
            damage = generate_damage(30, 50)
            damage = apply_critical(damage)
            enemy_hp -= damage
            print(f" Special attack deals {damage} damage!")

    else:
        print("Invalid option.")
        return player_turn(hero_hp, enemy_hp, potions)

    return hero_hp, enemy_hp, potions

def enemy_turn(hero_hp):
    damage = generate_damage(15, 20)
    damage = apply_critical(damage)
    hero_hp -= damage
    print(f"Enemy attacks and deals {damage} damage!")
    return hero_hp

def check_winner(hero_hp, enemy_hp):
    if hero_hp <= 0:
        print(" You lost!")
        return True
    elif enemy_hp <= 0:
        print(" You won!")
        return True
    return False

def game():
    hero_name = "Hero"
    enemy_name = "Enemy"

    hero_hp = 100
    enemy_hp = 120
    potions = 3

    while hero_hp > 0 and enemy_hp > 0:
        show_status(hero_name, hero_hp, enemy_name, enemy_hp)

        hero_hp, enemy_hp, potions = player_turn(hero_hp, enemy_hp, potions)

        if enemy_hp > 0:
            hero_hp = enemy_turn(hero_hp)

        if check_winner(hero_hp, enemy_hp):
            break

game()
