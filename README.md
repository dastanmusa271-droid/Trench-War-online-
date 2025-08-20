# Trench-War-online-
1.dünya savaşı mobil oyun 
|
--+--
  |using UnityEngine;

public class WeaponSystem : MonoBehaviour
{
    public GameObject bulletPrefab;
    public Transform firePoint;
    public float fireRate = 0.5f;
    float nextFireTime = 0f;

    void Update()
    {
        if (Input.GetButton("Fire1") && Time.time >= nextFireTime)
        {
            Fire();
            nextFireTime = Time.time + fireRate;
        }
    }

    void Fire()
    {
        Instantiate(bulletPrefab, firePoint.position, firePoint.rotation);
    }
}Time.timeusing UnityEngine;
using UnityEngine.SceneManagement;

public class GameManager : MonoBehaviour
{
    public static GameManager instance;

    public int score = 0;
    public int playerHealth = 100;

    void Awake()
    {
        if (instance == null)
            instance = this;
        else
            Destroy(gameObject);
    }

    public void AddScore(int amount)
    {
        score += amount;
        Debug.Log("Score: " + score);
    }

    public void PlayerHit(int damage)
    {
        playerHealth -= damage;
        if (playerHealth <= 0)
        {
            EndGame();
        }
    }

    void EndGame()
    {
        Debug.Log("Game Over!");
        SceneManager.LoadScene(SceneManager.GetActiveScene().name);
    }
}using UnityEngine;

public class PlayerController : MonoBehaviour
{
    public float moveSpeed = 5f;
    public float rotateSpeed = 200f;
    public GameObject bulletPrefab;
    public Transform firePoint;

    void Update()
    {
        // Hareket
        float move = Input.GetAxis("Vertical") * moveSpeed * Time.deltaTime;
        float rotate = Input.GetAxis("Horizontal") * rotateSpeed * Time.deltaTime;
        transform.Translate(0, 0, move);
        transform.Rotate(0, rotate, 0);

        // Ateş
        if (Input.GetKeyDown(KeyCode.Space))
        {
            Shoot();
        }
    }

    void Shoot()
    {
        Instantiate(bulletPrefab, firePoint.position, firePoint.rotation);
    }
}TrenchWarOnline_Lite/
│
├── Assets/
│   ├── Scenes/
│   │   └── Main.unity
│   ├── Scripts/
│   │   ├── PlayerController.cs
│   │   ├── EnemyAI.cs
│   │   ├── GameManager.cs
│   │   └── WeaponSystem.cs
│   ├── Models/
│   │   ├── tank_placeholder.fbx
│   │   ├── plane_placeholder.fbx
│   │   └── soldier_placeholder.fbx
│   ├── Textures/
│   │   ├── tank_texture.png
│   │   ├── plane_texture.png
│   │   └── soldier_texture.png
│   └── UI/
│       ├── HUD.prefab
│       └── crosshair.png
│
├── ProjectSettings/
│   └── ProjectSettings.asset
│
└── Packages/
    └── manifest.jsonMain.unityPlayerController.csEnemyAI.cs
TrenchWarOnline_Final/
│
├── Assets/
│   ├── Scenes/
│   │   └── Main.unity
│   ├── Scripts/
│   │   ├── PlayerController.cs
│   │   ├── EnemyAI.cs
│   │   ├── GameManager.cs
│   │   ├── WeaponSystem.cs
│   │   └── Soldier.cs
│   ├── Models/
│   │   ├── ally_soldier.fbx
│   │   └── central_soldier.fbx
│   ├── Textures/
│   │   ├── ally_uniform.png
│   │   └── central_uniform.png
│   └── UI/
│       ├── HUD.prefab
│       └── crosshair.png
│
└── ProjectSettings/Main.unityPlayerController.csEnemyAI.csGameManager.csWeaponSystem.csSoldier.csally_soldier.fbxcentral_soldier.fbxally_uniform.pngcrosshair.pngHUD.prefabusing UnityEngine;

public enum Faction { Allies, Central }

public class Soldier : MonoBehaviour
{
    public Faction faction;
    public int health = 100;
    public int damage = 10;

    public void TakeDamage(int amount)
    {
        health -= amount;
        if (health <= 0)
        {
            if (faction == Faction.Central)
                GameManager.instance.AddScore(10);

            Destroy(gameObject);
        }
    }
}using UnityEngine;

public class PlayerController : MonoBehaviour
{
    public float moveSpeed = 5f;
    public float rotateSpeed = 200f;
    public GameObject bulletPrefab;
    public Transform firePoint;
    public Soldier soldier;

    void Update()
    {
        float move = Input.GetAxis("Vertical") * moveSpeed * Time.deltaTime;
        float rotate = Input.GetAxis("Horizontal") * rotateSpeed * Time.deltaTime;

        transform.Translate(0, 0, move);
        transform.Rotate(0, rotate, 0);

        if (Input.GetKeyDown(KeyCode.Space))
        {
            Shoot();
        }
    }

    void Shoot()
    {
        GameObject bullet = Instantiate(bulletPrefab, firePoint.position, firePoint.rotation);
        Bullet b = bullet.GetComponent<Bullet>();
        b.SetShooter(soldier.faction);
    }
}using UnityEngine;

public class Bullet : MonoBehaviour
{
    public float speed = 20f;
    public int damage = 20;
    private Faction shooterFaction;

    void Update()
    {
        transform.Translate(Vector3.forward * speed * Time.deltaTime);
    }

    public void SetShooter(Faction faction)
    {
        shooterFaction = faction;
    }

    void OnCollisionEnter(Collision collision)
    {
        Soldier s = collision.gameObject.GetComponent<Soldier>();
        if (s != null && s.faction != shooterFaction)
        {
            s.TakeDamage(damage);
        }
        Destroy(gameObject);
    }
}s.factionusing UnityEngine;

public class EnemyAI : MonoBehaviour
{
    public Transform player;
    public float moveSpeed = 2f;
    private Soldier soldier;

    void Start()
    {
        soldier = GetComponent<Soldier>();
    }

    void Update()
    {
        if (player != null)
        {
            Vector3 direction = (player.position - transform.position).normalized;
            transform.Translate(direction * moveSpeed * Time.deltaTime, Space.World);
        }
    }
}central_uniform.png