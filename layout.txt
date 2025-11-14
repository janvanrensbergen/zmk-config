// Copyright 2023 QMK
// SPDX-License-Identifier: GPL-2.0-or-later

#include QMK_KEYBOARD_H
#include <stdio.h>

#define U_NP KC_NO // key is not present
#define U_NA KC_NO // present but not available for use
#define U_NU KC_NO // available but not used

enum layers { COLEMAK, NAV, NUM, SYM, FUN, MBO, MEDIA, MOUSE};

#define U_RDO SCMD(KC_Z)
#define U_PST LCMD(KC_V)
#define U_CPY LCMD(KC_C)
#define U_CUT LCMD(KC_X)
#define U_UND LCMD(KC_Z)

#define LCONTROL LCTL_T(KC_A)
#define LOPTION LALT_T(KC_R)
#define LCOMMAND LGUI_T(KC_S)
#define LSHIFT LSFT_T(KC_T)
#define RSHIFT RSFT_T(KC_N)
#define RCOMMAND RGUI_T(KC_E)
#define ROPTION RALT_T(KC_I)
#define RCONTROL RCTL_T(KC_O)

#define MEDIA_ESC LT(MEDIA, KC_ESC)
#define NAV_TAB   LT(NAV, KC_TAB)
#define MOUSE_SPC LT(MOUSE, KC_SPC)
#define SYM_ENT   LT(SYM, KC_ENT)
#define NUM_BSPC  LT(NUM, KC_BSPC)
#define FUN_DEL   LT(FUN, KC_DEL)

const uint16_t PROGMEM cpslk_combo[] = {LCONTROL, RCONTROL, COMBO_END};
combo_t key_combos[] = {
    COMBO(cpslk_combo, KC_CAPS),
};

const uint16_t PROGMEM keymaps[][MATRIX_ROWS][MATRIX_COLS] = {
  [COLEMAK] = LAYOUT_split_3x5_3(
      //,------------------------------------------------.                         ,--------------------------------------------------.
          KC_Q,    KC_W,     KC_F,    KC_P,     KC_G,                                  KC_J,     KC_L,     KC_U,    KC_Y,    KC_QUOT,
      //|--------+---------+--------+--------+-----------|                         |---------+---------+---------+---------+---------|
         LCONTROL,    LOPTION,  LCOMMAND, LSHIFT,  KC_D,                                  KC_H,    RSHIFT,  RCOMMAND, ROPTION, RCONTROL,
      //|--------+---------+--------+--------+-----------|                         |---------+---------+---------+---------+---------|
          KC_Z,    KC_X,     KC_C,     KC_V,      KC_B,                                KC_K,      KC_M,   KC_COMM,  KC_DOT,   KC_SLSH,
      //|--------+---------+--------+--------+-----------+------------|  |---------+---------+---------+---------+---------+---------|
                                           MEDIA_ESC, NAV_TAB, MOUSE_SPC,      SYM_ENT, NUM_BSPC, FUN_DEL
                                       //`--------------------------------'  `----------------------------'
    ),

  [NAV] = LAYOUT_split_3x5_3(
        //,--------------------------------------------.                    ,--------------------------------------------.
            QK_BOOT,   U_NA,    DT_PRNT,  DT_UP, DT_DOWN,                        U_RDO, U_PST,   U_CPY,   U_CUT,     U_UND,
        //|--------+--------+--------+--------+--------|                    |--------+--------+--------+--------+--------|
            KC_LCTL, KC_LALT,  KC_LGUI, KC_LSFT, U_NA,                         KC_CAPS, KC_LEFT, KC_DOWN, KC_UP,  KC_RGHT,
        //|--------+--------+--------+--------+--------|                    |--------+--------+--------+--------+--------|
            U_NA,    KC_ALGR, U_NA,    U_NA,    U_NA,                          KC_INS, KC_HOME, KC_PGDN, KC_PGUP, KC_END,
        //|--------+--------+--------+--------+--------+--------|  |--------+--------+--------+--------+--------+--------|
                                                 U_NA,    U_NA,    U_NA,      KC_ENT, KC_BSPC, KC_DEL
                                             //`--------------------------'  `--------------------------'
  ),
  [NUM] = LAYOUT_split_3x5_3(
        //,---------------------------------------------.                    ,---------------------------------------------.
             KC_LBRC,  KC_7,    KC_8,    KC_9,  KC_RBRC,                        U_NA,    U_NA,    U_NA,    U_NA,   QK_BOOT,
        //|---------+--------+--------+--------+--------|                    |--------+--------+--------+--------+--------+|
             KC_SCLN,  KC_4,    KC_5,    KC_6,   KC_EQL,                        U_NA,   KC_LSFT, KC_LGUI, KC_LALT, KC_LCTL,
        //|---------+--------+--------+--------+--------|                    |--------+--------+--------+--------+--------+|
             KC_GRV,   KC_1,    KC_2,    KC_3,   KC_BSLS,                       U_NA,   U_NA,    U_NA,   KC_ALGR,  U_NA,
        //|---------+--------+--------+--------+--------+--------|  |--------+--------+--------+--------+--------+--------+|
                                                 KC_DOT,  KC_0,  KC_MINS,      U_NA,    U_NA,    U_NA
                                             //`--------------------------'  `--------------------------'
  ),
  [SYM] = LAYOUT_split_3x5_3(
        //,---------------------------------------------.                    ,-----------------------------------------------.
            KC_LCBR, KC_AMPR, KC_ASTR, KC_LPRN,  KC_RCBR,                       U_NA,    U_NA,    U_NA,    U_NA,    QK_BOOT,
        //|---------+--------+--------+--------+--------|                    |--------+--------+--------+--------+----------|
            KC_COLN, KC_DLR,  KC_PERC, KC_CIRC, KC_PLUS,                        U_NA,  KC_LSFT, KC_LGUI, KC_LALT, KC_LCTL,
        //|---------+--------+--------+--------+--------|                    |--------+--------+--------+--------+----------|
            KC_TILD, KC_EXLM, KC_AT,   KC_HASH, KC_PIPE,                        U_NA,    U_NA,    U_NA,    KC_ALGR,   U_NA,
        //|---------+--------+--------+--------+--------+--------|  |--------+--------+--------+--------+--------+----------|
                                                 KC_LPRN, KC_RPRN, KC_UNDS,      U_NA,     U_NA,    U_NA
                                             //`--------------------------'  `--------------------------'
  ),
  [FUN] = LAYOUT_split_3x5_3(
        //,-------------------------------------------.                    ,--------------------------------------------.
           KC_F12,  KC_F7,   KC_F8,   KC_F9,  KC_PSCR,                        U_NA,    U_NA,    U_NA,    U_NA,  QK_BOOT,
        //|-------+--------+--------+--------+--------|                    |--------+--------+--------+--------+--------|
           KC_F11,  KC_F4,   KC_F5,   KC_F6,  KC_SCRL,                        U_NA,  KC_LSFT, KC_LGUI, KC_LALT, KC_LCTL,
        //|-------+--------+--------+--------+--------|                    |--------+--------+--------+--------+--------|
           KC_F10,  KC_F1,   KC_F2,   KC_F3,  KC_PAUS,                        U_NA,     U_NA,  U_NA,   KC_ALGR, U_NA,
        //|-------+--------+--------+--------+--------+--------|  |--------+--------+--------+--------+--------+--------|
                                                KC_APP,  KC_SPC,  KC_TAB,      U_NA,    U_NA,    U_NA
                                             //`--------------------------'  `--------------------------'
  ),
  [MBO] = LAYOUT_split_3x5_3(
       //,---------------------------------------------.                    ,--------------------------------------------.
           KC_TRNS, KC_TRNS, KC_TRNS, KC_TRNS, KC_TRNS,                       KC_TRNS, KC_TRNS, KC_TRNS, KC_TRNS, KC_TRNS,
       //|---------+--------+--------+--------+--------|                    |--------+--------+--------+--------+--------|
           KC_LGUI, KC_LALT, KC_LCTL, KC_LSFT, KC_TRNS,                       KC_TRNS, KC_LGUI, KC_LSFT, KC_LCTL, KC_LALT,
       //|---------+--------+--------+--------+--------|                    |--------+--------+--------+--------+--------|
           U_RDO,   U_PST,   U_CPY,   U_CUT,   U_UND,                         U_RDO,   U_PST,   U_CPY,   U_CUT,   U_UND,
       //|---------+--------+--------+--------+--------+--------|  |--------+--------+--------+--------+--------+--------|
                                              MS_BTN2, MS_BTN3, MS_BTN1,     MS_BTN1, MS_BTN3, MS_BTN2
                                            //`--------------------------'  `--------------------------'
  ),
  [MEDIA] = LAYOUT_split_3x5_3(
        //,-------------------------------------------.                    ,------------------------------------------------.
           QK_BOOT,   U_NA,    U_NA,    U_NA,    U_NA,                       U_NA,     U_NA,    U_NA,    U_NA,     U_NA,
        //|-------+--------+--------+--------+--------|                    |--------+--------+--------+--------+-----------|
           KC_LGUI, KC_LALT, KC_LCTL, KC_LSFT, U_NA,                         U_NU,    KC_MPRV, KC_VOLD, KC_VOLU, KC_MNXT,
        //|-------+--------+--------+--------+--------|                    |--------+--------+--------+--------+-----------|
           U_NA,    KC_ALGR, U_NA,    U_NA,    U_NA,                         U_NU,    U_NU,    U_NU,    U_NU,    U_NU,
        //|-------+--------+--------+--------+--------+--------|  |--------+--------+--------+--------+--------+-----------|
                                                U_NA,    U_NA,    U_NA,        KC_MSTP, KC_MPLY, KC_MUTE
                                             //`--------------------------'  `--------------------------'
  ),
  [MOUSE] = LAYOUT_split_3x5_3(
        //,-------------------------------------------.                    ,---------------------------------------------.
           QK_BOOT,   U_NA,    U_NA,    U_NA,    U_NA,                         U_PST,   U_CPY,   U_CUT,   U_UND,  U_RDO,
        //|-------+--------+--------+--------+--------|                    |--------+--------+--------+--------+---------|
           KC_LCTL, KC_LALT,  KC_LGUI, KC_LSFT, U_NA,                         U_NU,   MS_LEFT, MS_DOWN, MS_UP, MS_RGHT,
        //|-------+--------+--------+--------+--------|                    |--------+--------+--------+--------+---------|
           U_NA,    KC_ALGR, U_NA,    U_NA,    U_NA,                         U_NU,    MS_WHLL, MS_WHLD, MS_WHLU, MS_WHLR,
        //|-------+--------+--------+--------+--------+--------|  |--------+--------+--------+--------+--------+---------|
                                                U_NA,    U_NA,    U_NA,       MS_BTN1, MS_BTN3, MS_BTN2
                                             //`--------------------------'  `--------------------------'
  )
};

uint16_t get_tapping_term(uint16_t keycode, keyrecord_t *record) {
    switch (keycode) {
        case NAV_TAB:
            return 150;
        default:
            return TAPPING_TERM;
    }
}

void keyboard_pre_init_user(void) {
  // Set our LED pin as output
  setPinOutput(24);
  // Turn the LED off
  // (Due to technical reasons, high is off and low is on)
  writePinHigh(24);
}

void caps_word_set_user(bool active) {
  setPinOutput(24);
  if (active) {
      writePinLow(24);
  } else {
      writePinHigh(24);
  }
}


