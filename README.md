# WebXR Expression Tracking

## Introduction
Expression tracking is a technology that reports a set of expressions of the current user. The expressions report how much a portion of the face or an eye move. They don't report actual positions or other real world data.

## Use cases
The main use case is to render the user's face and eyes using an avatar for increased social presence.
This technology will NOT:
* allow rendering of the user's actual face
* give precise information where the user is looking
* allow virtual interaction with the user's face (ie Makeup, hats, etc)

## Proposed API shape
This API will define an extensive set of expression and will on a per frame basis, report which ones were detected and how strong they are.
For instance, if the device's eye tracking is functional and the user looks left, it will return that both eyes are looking left.

```webidl
enum XRExpression {
  "brow_lowerer_left",
  "brow_lowerer_right",
  "cheek_puff_left",
  "cheek_puff_right",
  "cheek_raiser_left",
  "cheek_raiser_right",
  "cheek_suck_left",
  "cheek_suck_right",
  "chin_raiser_bottom",
  "chin_raiser_top",
  "dimpler_left",
  "dimpler_right",
  "eyes_closed_left",
  "eyes_closed_right",
  "eyes_look_down_left",
  "eyes_look_down_right",
  "eyes_look_left_left",
  "eyes_look_left_right",
  "eyes_look_right_left",
  "eyes_look_right_right",
  "eyes_look_up_left",
  "eyes_look_up_right",
  "inner_brow_raiser_left",
  "inner_brow_raiser_right",
  "jaw_drop",
  "jaw_sideways_left",
  "jaw_sideways_right",
  "jaw_thrust",
  "lid_tightener_left",
  "lid_tightener_right",
  "lip_corner_depressor_left",
  "lip_corner_depressor_right",
  "lip_corner_puller_left",
  "lip_corner_puller_right",
  "lip_funneler_left_bottom",
  "lip_funneler_left_top",
  "lip_funneler_right_bottom",
  "lip_funneler_right_top",
  "lip_pressor_left",
  "lip_pressor_right",
  "lip_pucker_left",
  "lip_pucker_right",
  "lip_stretcher_left",
  "lip_stretcher_right",
  "lip_suck_left_bottom",
  "lip_suck_left_top",
  "lip_suck_right_bottom",
  "lip_suck_right_top",
  "lip_tightener_left",
  "lip_tightener_right",
  "lips_toward",
  "lower_lip_depressor_left",
  "lower_lip_depressor_right",
  "mouth_left",
  "mouth_right",
  "nose_wrinkler_left",
  "nose_wrinkler_right",
  "outer_brow_raiser_left",
  "outer_brow_raiser_right",
  "upper_lid_raiser_left",
  "upper_lid_raiser_right",
  "upper_lip_raiser_left",
  "upper_lip_raiser_right"
};

interface XRExpressions {
    iterable<XRExpression, float>;

    readonly attribute unsigned long size;
    float get(XRExpression key);
};

partial interface XRFrame {
    readonly attribute XRExpressions? expressions;
}

```

## Background/Rationale
This API is inspired by the OpenXR face extensions.

## Security/privacy implications
Face tracking exposes sensitive sensor data.
Because of this, the user agent must ask the user for their permission when a session is asking for this feature (much like WebXR and WebXR hand tracking).
In addition, sensitive values such as eye position must be rounded.
