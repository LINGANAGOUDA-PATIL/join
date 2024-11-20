# join
join abap 

*&---------------------------------------------------------------------*
*& Report ZPGM_CR3_JOIN
*&---------------------------------------------------------------------*
*&
*&---------------------------------------------------------------------*
REPORT ZPGM_CR3_JOIN.

TYPES:BEGIN OF LTY_FINAL,
        ONO   TYPE ZDEONO_277,
        ODATE TYPE ZDEODATE_277,
        PM    TYPE ZDEPM_277,
        CUR   TYPE ZDECUR_277,
        OIN   TYPE ZDEOITMNO_277,
        ICOST TYPE ZDEICOST_277,
      END OF LTY_FINAL.

DATA:LT_FINAL TYPE TABLE OF LTY_FINAL.
DATA:LWA_FINAL TYPE LTY_FINAL.

DATA:LV_ONO TYPE ZDEONO_277.

SELECTION-SCREEN : begin of block c1 with frame TITLE text-001.
SELECT-OPTIONS : S_ONO FOR LV_ONO.
SELECTION-SCREEN: end of BLOCK c1.



write: / 'order number', 15 'order date', 27 'payment mode', 41 'currency',
51 'order item no', 66 'item cost'.

SELECT H~ONO H~ODATE H~PM H~CUR I~OIN I~ICOST
FROM ZOH_277 AS H JOIN ZOI_277 AS I
ON H~ONO = I~ONO
  INTO TABLE LT_FINAL
  WHERE H~ONO IN S_ONO.

**left outer jon
*SELECT H~ONO H~ODATE H~PM H~CUR I~OIN I~ICOST
*FROM ZOH_277 AS H left JOIN ZOI_277 AS I
*ON H~ONO = I~ONO
*INTO TABLE LT_FINAL
*  WHERE H~ONO IN S_ONO.

LOOP AT LT_FINAL INTO LWA_FINAL.
  WRITE : / LWA_FINAL-ONO UNDER 'order number', LWA_FINAL-ODATE UNDER 'order date', LWA_FINAL-PM UNDER 'payment mode',
   LWA_FINAL-CUR under 'currency', LWA_FINAL-OIN under 'order item no', LWA_FINAL-ICOST under 'item cost'.
ENDLOOP.
