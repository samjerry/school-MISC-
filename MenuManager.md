using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.UI;

public class MenuManager : MonoBehaviour {

	public Button Yes;
	public Button No;

	private GameObject _restartMenu;

	public bool isDead; 

	void Start(){
		_restartMenu = GameObject.Find ("RestartMenu");
		_restartMenu.SetActive (false); 
	}
	void Update(){
		if (isDead) {
			_restartMenu.SetActive (true); 
		}
	}
}
