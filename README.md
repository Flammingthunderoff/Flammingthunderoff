using UnityEngine;

public class CharacterController : MonoBehaviour
{
    public enum CharacterType { Yakedo, Shensoku }
    public CharacterType characterType;

    public float health = 100f;
    public float moveSpeed = 5f;

    private float attackCooldown = 0f;

    // Update is called once per frame
    void Update()
    {
        Move();
        HandleAttack();
    }

    void Move()
    {
        float horizontal = Input.GetAxis("Horizontal");
        float vertical = Input.GetAxis("Vertical");
        Vector3 movement = new Vector3(horizontal, 0f, vertical) * moveSpeed * Time.deltaTime;
        transform.Translate(movement);
    }

    void HandleAttack()
    {
        // Attaque de base
        if (Input.GetButtonDown("Fire1") && attackCooldown <= 0f)
        {
            if (characterType == CharacterType.Yakedo)
            {
                YakedoFireAttack();
            }
            else if (characterType == CharacterType.Shensoku)
            {
                ShensokuThunderAttack();
            }
            attackCooldown = 1f; // Attaque toutes les 1 secondes (exemple)
        }
        attackCooldown -= Time.deltaTime;
    }

    void YakedoFireAttack()
    {
        Debug.Log("Yakedo attaque avec un coup de feu !");
        // Code pour l'attaque de feu, comme des flammes qui sortent du personnage
        // Ajouter un effet visuel de flamme
    }

    void ShensokuThunderAttack()
    {
        Debug.Log("Shensoku attaque avec un éclair !");
        // Code pour l'attaque électrique
        // Ajouter un effet visuel d'éclair qui frappe un ennemi
    }
}void YakedoFireAttack()
{
    Debug.Log("Yakedo lance une vague de feu !");
    // Créer un effet de vague de feu ici (par exemple un cône ou une ligne de feu)
    Collider[] hitEnemies = Physics.OverlapSphere(transform.position, 5f, LayerMask.GetMask("Enemy"));
    foreach (Collider enemy in hitEnemies)
    {
        enemy.GetComponent<Enemy>().TakeDamage(20f);  // Appliquer des dégâts
    }
}void ShensokuThunderAttack()
{
    Debug.Log("Shensoku lance un éclair !");
    // Créer un effet visuel d'éclair
    Collider[] hitEnemies = Physics.OverlapSphere(transform.position, 5f, LayerMask.GetMask("Enemy"));
    foreach (Collider enemy in hitEnemies)
    {
        enemy.GetComponent<Enemy>().TakeDamage(15f);  // Appliquer des dégâts
    }
}using UnityEngine;
using UnityEngine.UI;

public class HealthBar : MonoBehaviour
{
    public Image healthBar;
    public CharacterController character;

    void Update()
    {
        healthBar.fillAmount = character.health / 100f;  // Remplir la barre en fonction de la vie
    }
}
